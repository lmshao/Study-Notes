# FFmpeg 学习笔记

>参考：   
>1. [http://blog.csdn.net/leixiaohua1020](http://blog.csdn.net/leixiaohua1020)   
>2. FFmepg project 

## 1. 结构体

### 1.1 Protocol

**AVIOContext** / **URLProtocol** / **URLContext**   

>AVIOContext，URLProtocol，URLContext主要存储视音频使用的协议的类型以及状态。URLProtocol存储输入视音频使用的封装格式。每种协议都对应一个URLProtocol结构。（注意：FFMPEG中文件也被当做一种协议“file”）   


### 1.2 Format

**AVFormatContext** / **AVInputFormat**   

>AVFormatContext主要存储视音频封装格式中包含的信息；AVInputFormat存储输入视音频使用的封装格式。每种视音频封装格式都对应一个AVInputFormat 结构。

#### 1.2.1 AVFormatContext
`#include <avformat.h>`
部分成员
```c
typedef struct AVFormatContext {
    /* Set by avformat_alloc_context() */
    const AVClass *av_class;

    /* 输入容器的格式，Demuxing only, set by avformat_open_input(). */
    struct AVInputFormat *iformat;

    /* 输出容器格式， Muxing only, must be set by the caller before avformat_write_header(). */
    struct AVOutputFormat *oformat;

    /* 
     * 特定格式的私有数据
     * - muxing: set by avformat_write_header()
     * - demuxing: set by avformat_open_input()
     */
    void *priv_data;

    /**
     * I/O context.
     *
     * - demuxing: either set by the user before avformat_open_input() (then
     *             the user must close it manually) or set by avformat_open_input().
     * - muxing: set by the user before avformat_write_header(). The caller must
     *           take care of closing / freeing the IO context.
     *
     */
    AVIOContext *pb;

    /* 流信息 */
    /* 流属性标识. A combination of AVFMTCTX_*. Set by libavformat.  */
    int ctx_flags;

    /**
     * AVFormatContext.streams 中元素个数
     * Set by avformat_new_stream(), must not be modified by any other code.
     */
    unsigned int nb_streams;
    /**
     * 文件中流列表. 新的流使用 avformat_new_stream()创建
     *
     * - demuxing: streams are created by libavformat in avformat_open_input().
     *             If AVFMTCTX_NOHEADER is set in ctx_flags, then new streams may also
     *             appear in av_read_frame().
     * - muxing: streams are created by the user before avformat_write_header().
     *
     * Freed by libavformat in avformat_free_context().
     */
    AVStream **streams;

    /**
     * 输入输出文件名
     *
     * - demuxing: set by avformat_open_input()
     * - muxing: may be set by the caller before avformat_write_header()
     */
    char filename[1024];

    /**
     * 第一个帧的位置, 
     * in AV_TIME_BASE fractional seconds. NEVER set this value directly:
     * It is deduced from the AVStream values.
     *
     * Demuxing only, set by libavformat.
     */
    int64_t start_time;

    /**
     * 时长us, in AV_TIME_BASE fractional
     * seconds. Only set this value if you know none of the individual stream
     * durations and also do not set any of them. This is deduced from the
     * AVStream values if not set.
     *
     * Demuxing only, set by libavformat.
     */
    int64_t duration;

    /**
     * 总码率 bit/s, 0 if not
     * available. Never set it directly if the file_size and the
     * duration are known as FFmpeg can compute it automatically.
     */
    int64_t bit_rate;

    unsigned int packet_size;
    int max_delay;

    /**
     * Flags modifying the (de)muxer behaviour. A combination of AVFMT_FLAG_*.
     * Set by the user before avformat_open_input() / avformat_write_header().
     */
    int flags;


    /**
     * 从输入读取的用于确定输入容器格式的数据的最大大小。
     * Demuxing only, set by the caller before avformat_open_input().
     */
    int64_t probesize;

    /**
     * 从输入读取的数据的最大延时 in avformat_find_stream_info().
     * Demuxing only, set by the caller before avformat_find_stream_info().
     * Can be set to 0 to let avformat choose using a heuristic.
     */
    int64_t max_analyze_duration;

    const uint8_t *key;
    int keylen;

    unsigned int nb_programs;
    AVProgram **programs;

    /**
     * 视频解码器ID
     * Demuxing: Set by user.
     */
    enum AVCodecID video_codec_id;

    /**
     * 音频解码器ID
     * Demuxing: Set by user.
     */
    enum AVCodecID audio_codec_id;

    /**
     * 字幕解码器ID
     * Demuxing: Set by user.
     */
    enum AVCodecID subtitle_codec_id;

    unsigned int max_index_size;

    unsigned int max_picture_buffer;

    /* 章节数 */
    unsigned int nb_chapters;
    AVChapter **chapters;

    /**
     * 整个文件元数据
     *
     * - demuxing: set by libavformat in avformat_open_input()
     * - muxing: may be set by the caller before avformat_write_header()
     *
     * Freed by libavformat in avformat_free_context().
     */
    AVDictionary *metadata;

    /**
     * 流开始时间us, 真实世界时间 since the Unix epoch (00:00 1st January 1970).
     * - muxing: Set by the caller before avformat_write_header(). If set to
     *           either 0 or AV_NOPTS_VALUE, then the current wall-time will
     *           be used.
     * - demuxing: Set by libavformat. AV_NOPTS_VALUE if unknown. Note that
     *             the value may become known after some number of frames
     *             have been received.
     */
    int64_t start_time_realtime;

    int fps_probe_size;

    int error_recognition;

    AVIOInterruptCB interrupt_callback;

    int debug;
    int64_t max_interleave_delta;

    int strict_std_compliance;

    int event_flags;

    int max_ts_probe;

    int avoid_negative_ts;

    int ts_id;

    int audio_preload;

    int max_chunk_duration;

    int max_chunk_size;

    int use_wallclock_as_timestamps;

    int avio_flags;

    enum AVDurationEstimationMethod duration_estimation_method;

    int64_t skip_initial_bytes;

    unsigned int correct_ts_overflow;

    int seek2any;

    int flush_packets;

    int probe_score;

    int format_probesize;

    char *codec_whitelist;

    char *format_whitelist;

    AVFormatInternal *internal;

    int io_repositioned;


    AVCodec *video_codec;

    AVCodec *audio_codec;

    AVCodec *subtitle_codec;

    AVCodec *data_codec;


    int metadata_header_padding;

    /**
     * User data.
     * This is a place for some private data of the user.
     */
    void *opaque;

    /**
     * Callback used by devices to communicate with application.
     */
    av_format_control_message control_message_cb;

    /**
     * Output timestamp offset, in microseconds.
     * Muxing: set by user via AVOptions (NO direct access)
     */
    int64_t output_ts_offset;

    /**
     * dump format separator.
     * can be ", " or "\n      " or anything else
     * Code outside libavformat should access this field using AVOptions
     * (NO direct access).
     * - muxing: Set by user.
     * - demuxing: Set by user.
     */
    uint8_t *dump_separator;

    /**
     * Forced Data codec_id.
     * Demuxing: Set by user.
     */
    enum AVCodecID data_codec_id;


    char *protocol_whitelist;

    int (*io_open)(struct AVFormatContext *s, AVIOContext **pb, const char *url,
                   int flags, AVDictionary **options);

    void (*io_close)(struct AVFormatContext *s, AVIOContext *pb);

    char *protocol_blacklist;
} AVFormatContext;
```


### 1.3 Codec

**AVStream** / **AVCodecContext**   

>每个AVStream存储一个视频/音频流的相关数据；每个AVStream对应一个AVCodecContext，存储该视频/音频流使用解码方式的相关数据；每个AVCodecContext中对应一个AVCodec，包含该视频/音频对应的解码器。每种解码器都对应一个AVCodec结构。

### 1.4 Data

**AVPacket** / **AVFrame**   

>视频的话，每个结构一般是存一帧；音频可能有好几帧，解码前数据：AVPacket；解码后数据：AVFrame。

#### 1.4.1 AVFrame

`libavutil/frame.h`   
  
部分成员
```c 
typedef struct AVFrame {
#define AV_NUM_DATA_POINTERS 8

    /* 解码后原始数据 */
    uint8_t *data[AV_NUM_DATA_POINTERS];

    /* 视频：每个图像行的字节大小；音频：每个plane的字节大小 */
    int linesize[AV_NUM_DATA_POINTERS];

    /* 仅用于planar audio */
    uint8_t **extended_data;

    /* 视频帧宽高 */
    int width, height;

    /* 此AVFrame结构包含的音频采样的数量 */
    int nb_samples;

    /**
     * 帧格式，-1表示未知，视频对应AVPixelFormat，音频对应AVSampleFormat */
    int format;

    /* 是否为关键帧，1-关键帧 */
    int key_frame;

    /* 图像类型（I,P,B） */
    enum AVPictureType pict_type;

    /* 视频宽高比（16:9，4:3）, 0-未知，1-未指定 */
    AVRational sample_aspect_ratio;

    /* 显示时间戳 */
    int64_t pts;

#if FF_API_PKT_PTS
    /* 已弃用 */
    int64_t pkt_pts;
#endif

    int64_t pkt_dts;

    /* 编码图像序号 */
    int coded_picture_number;

    /* 显示帧序号 */
    int display_picture_number;

    /* 质量 (between 1 (good) and FF_LAMBDA_MAX (bad)) */
    int quality;

    /* 用户私有数据 */
    void *opaque;

    /* 解码时，指示图像要被延时多少帧，extra_delay = repeat_pict / (2*fps) */
    int repeat_pict;

    /* 是否隔行扫描 */
    int interlaced_frame;

    /* 如果隔行扫描，首先显示上部分 */
    int top_field_first;

    /* 告诉用户应用程序调色板已从上一帧变换 */
    int palette_has_changed;

    int64_t reordered_opaque;

    /* 音频采样率 */
    int sample_rate;

    /* 音频声道布局 */
    uint64_t channel_layout;

    /* extended_buf中元素数量 */
    int        nb_extended_buf;

    AVFrameSideData **side_data;
    int            nb_side_data;

    /**
     * Frame flags, a combination of @ref lavu_frame_flags
     */
    int flags;

    /**
     * MPEG vs JPEG YUV 颜色范围.
     * It must be accessed using av_frame_get_color_range() and
     * av_frame_set_color_range().
     * - encoding: Set by user
     * - decoding: Set by libavcodec
     */
    enum AVColorRange color_range;

    enum AVColorPrimaries color_primaries;

    enum AVColorTransferCharacteristic color_trc;

    /**
     * YUV colorspace type.
     * It must be accessed using av_frame_get_colorspace() and
     * av_frame_set_colorspace().
     * - encoding: Set by user
     * - decoding: Set by libavcodec
     */
    enum AVColorSpace colorspace;

	/* 色度样本的位置 */
    enum AVChromaLocation chroma_location;

    AVDictionary *metadata;

    /* 音频声道数量 */
    int channels;

    /* 包含压缩数据相应包的大小 */
    int pkt_size;

    /* QP表 */
    attribute_deprecated
    int8_t *qscale_table;

    attribute_deprecated
    int qstride;

    attribute_deprecated
    int qscale_type;
} AVFrame;
```

1. data[]   
对于packed格式的数据（例如RGB24），会存到data[0]里面。   
对于planar格式的数据（例如YUV420P），则会分开成data[0]，data[1]，data[2]...（YUV420P中data[0]存Y，data[1]存U，data[2]存V） 
2. qscale_table   
QP表指向一块内存，里面存储的是每个宏块的QP值。宏块的标号是从左往右，一行一行的来的。每个宏块对应1个QP。   
qscale_table[0]就是第1行第1列宏块的QP值；qscale_table[2]就是第1行第3列宏块的QP值。以此类推...   
宏块的个数用下式计算：   
注：宏块大小是16x16的。   
每行宏块数：   
`int mb_stride = pCodecCtx->width/16+1`     
宏块的总数：     
`int mb_sum = ((pCodecCtx->height+15)>>4)*(pCodecCtx->width/16+1)```




