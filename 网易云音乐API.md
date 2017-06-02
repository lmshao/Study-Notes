# 搜索歌曲
POST http://music.163.com/api/search/get?s=青花瓷&limit=3&type=1&offset=0&appver=1.5.2   
```python
r = requests.post('http://music.163.com/api/search/get',data={'s':'青花瓷','limit':3,'sub':'false','type':1,'offset':0,'appver':'1.5.2'})
print(r.text)
```

```json
{
    "result": {
        "songs": [
            {
                "id": 185811,
                "name": "青花瓷",
                "artists": [
                    {
                        "id": 6452,
                        "name": "周杰伦",
                        "picUrl": null,
                        "alias": [],
                        "albumSize": 0,
                        "picId": 0,
                        "img1v1Url": "http://p1.music.126.net/6y-UleORITEDbvrOLV0Q8A==/5639395138885805.jpg",
                        "img1v1": 0,
                        "trans": null
                    }
                ],
                "album": {
                    "id": 18886,
                    "name": "我很忙",
                    "artist": {
                        "id": 0,
                        "name": "",
                        "picUrl": null,
                        "alias": [],
                        "albumSize": 0,
                        "picId": 0,
                        "img1v1Url": "http://p1.music.126.net/6y-UleORITEDbvrOLV0Q8A==/5639395138885805.jpg",
                        "img1v1": 0,
                        "trans": null
                    },
                    "publishTime": 1193846400000,
                    "size": 10,
                    "copyrightId": 1007,
                    "status": 3,
                    "picId": 60473139533046
                },
                "duration": 239000,
                "copyrightId": 1007,
                "status": 0,
                "alias": [],
                "rtype": 0,
                "ftype": 0,
                "mvid": 284139,
                "fee": 8,
                "rUrl": null
            },
            {
                "id": 421563801,
                "name": "青花瓷",
                "artists": [
                    {
                        "id": 6452,
                        "name": "周杰伦",
                        "picUrl": null,
                        "alias": [],
                        "albumSize": 0,
                        "picId": 0,
                        "img1v1Url": "http://p1.music.126.net/6y-UleORITEDbvrOLV0Q8A==/5639395138885805.jpg",
                        "img1v1": 0,
                        "trans": null
                    }
                ],
                "album": {
                    "id": 34780604,
                    "name": "K情歌10",
                    "artist": {
                        "id": 0,
                        "name": "",
                        "picUrl": null,
                        "alias": [],
                        "albumSize": 0,
                        "picId": 0,
                        "img1v1Url": "http://p1.music.126.net/6y-UleORITEDbvrOLV0Q8A==/5639395138885805.jpg",
                        "img1v1": 0,
                        "trans": null
                    },
                    "publishTime": 1361462400007,
                    "size": 45,
                    "copyrightId": 7001,
                    "status": 3,
                    "picId": 1424967082830247
                },
                "duration": 239542,
                "copyrightId": 7001,
                "status": 0,
                "alias": [],
                "rtype": 0,
                "ftype": 0,
                "mvid": 0,
                "fee": 8,
                "rUrl": null
            },
            {
                "id": 412327311,
                "name": "青花瓷 (Live)",
                "artists": [
                    {
                        "id": 6452,
                        "name": "周杰伦",
                        "picUrl": null,
                        "alias": [],
                        "albumSize": 0,
                        "picId": 0,
                        "img1v1Url": "http://p1.music.126.net/6y-UleORITEDbvrOLV0Q8A==/5639395138885805.jpg",
                        "img1v1": 0,
                        "trans": null
                    }
                ],
                "album": {
                    "id": 34685590,
                    "name": "魔天伦 世界巡回演唱会",
                    "artist": {
                        "id": 0,
                        "name": "",
                        "picUrl": null,
                        "alias": [],
                        "albumSize": 0,
                        "picId": 0,
                        "img1v1Url": "http://p1.music.126.net/6y-UleORITEDbvrOLV0Q8A==/5639395138885805.jpg",
                        "img1v1": 0,
                        "trans": null
                    },
                    "publishTime": 1462809600007,
                    "size": 22,
                    "copyrightId": 1007,
                    "status": 3,
                    "picId": 1398578800308223
                },
                "duration": 238386,
                "copyrightId": 1007,
                "status": 0,
                "alias": [],
                "rtype": 0,
                "ftype": 0,
                "mvid": 5326091,
                "fee": 8,
                "rUrl": null
            }
        ],
        "songCount": 160
    },
    "code": 200
}
```

## 获取歌曲ID

```python
r.text.replace('null','\'\'')
t = json.loads(r.text)
print(t.get('result').get('songs')[0].get('id'))
```

# 获取歌曲信息

GET http://music.163.com/api/song/detail/?id=185811&ids=[185811]

```json
{
    "songs": [
        {
            "name": "青花瓷",
            "id": 185811,
            "position": 3,
            "alias": [],
            "status": 0,
            "fee": 8,
            "copyrightId": 1007,
            "disc": "",
            "no": 3,
            "artists": [
                {
                    "name": "周杰伦",
                    "id": 6452,
                    "picId": 0,
                    "img1v1Id": 0,
                    "briefDesc": "",
                    "picUrl": "http://p1.music.126.net/6y-UleORITEDbvrOLV0Q8A==/5639395138885805.jpg",
                    "img1v1Url": "http://p1.music.126.net/6y-UleORITEDbvrOLV0Q8A==/5639395138885805.jpg",
                    "albumSize": 0,
                    "alias": [],
                    "trans": "",
                    "musicSize": 0
                }
            ],
            "album": {
                "name": "我很忙",
                "id": 18886,
                "type": "专辑",
                "size": 10,
                "picId": 60473139533046,
                "blurPicUrl": "http://p1.music.126.net/0tWIPPsjYexJOvRqazMw6A==/60473139533046.jpg",
                "companyId": 0,
                "pic": 60473139533046,
                "picUrl": "http://p1.music.126.net/0tWIPPsjYexJOvRqazMw6A==/60473139533046.jpg",
                "publishTime": 1193846400000,
                "description": "",
                "tags": "",
                "company": "杰威尔音乐",
                "briefDesc": "",
                "artist": {
                    "name": "",
                    "id": 0,
                    "picId": 0,
                    "img1v1Id": 0,
                    "briefDesc": "",
                    "picUrl": "http://p1.music.126.net/6y-UleORITEDbvrOLV0Q8A==/5639395138885805.jpg",
                    "img1v1Url": "http://p1.music.126.net/6y-UleORITEDbvrOLV0Q8A==/5639395138885805.jpg",
                    "albumSize": 0,
                    "alias": [],
                    "trans": "",
                    "musicSize": 0
                },
                "songs": [],
                "alias": [],
                "status": 3,
                "copyrightId": 1007,
                "commentThreadId": "R_AL_3_18886",
                "artists": [
                    {
                        "name": "周杰伦",
                        "id": 6452,
                        "picId": 0,
                        "img1v1Id": 0,
                        "briefDesc": "",
                        "picUrl": "http://p1.music.126.net/6y-UleORITEDbvrOLV0Q8A==/5639395138885805.jpg",
                        "img1v1Url": "http://p1.music.126.net/6y-UleORITEDbvrOLV0Q8A==/5639395138885805.jpg",
                        "albumSize": 0,
                        "alias": [],
                        "trans": "",
                        "musicSize": 0
                    }
                ],
                "subType": "录音室版"
            },
            "starred": false,
            "popularity": 100,
            "score": 100,
            "starredNum": 0,
            "duration": 239000,
            "playedNum": 0,
            "dayPlays": 0,
            "hearTime": 0,
            "ringtone": "600902000006889088",
            "crbt": "e93f07bd4132712ed6e21dc3f37b4078",
            "audition": null,
            "copyFrom": "",
            "commentThreadId": "R_SO_4_185811",
            "rtUrl": null,
            "ftype": 0,
            "rtUrls": [],
            "copyright": 1,
            "hMusic": {
                "name": null,
                "id": 99228548,
                "size": 9576642,
                "extension": "mp3",
                "sr": 44100,
                "dfsId": 0,
                "bitrate": 320000,
                "playTime": 239000,
                "volumeDelta": -0.000265076
            },
            "mMusic": {
                "name": null,
                "id": 99228549,
                "size": 4788398,
                "extension": "mp3",
                "sr": 44100,
                "dfsId": 0,
                "bitrate": 160000,
                "playTime": 239000,
                "volumeDelta": -0.000265076
            },
            "lMusic": {
                "name": null,
                "id": 99228550,
                "size": 2873100,
                "extension": "mp3",
                "sr": 44100,
                "dfsId": 0,
                "bitrate": 96000,
                "playTime": 239000,
                "volumeDelta": -0.000265076
            },
            "bMusic": {
                "name": null,
                "id": 99228550,
                "size": 2873100,
                "extension": "mp3",
                "sr": 44100,
                "dfsId": 0,
                "bitrate": 96000,
                "playTime": 239000,
                "volumeDelta": -0.000265076
            },
            "rtype": 0,
            "rurl": null,
            "mvid": 284139,
            "mp3Url": null
        }
    ],
    "equalizers": {
        "185811": "pop"
    },
    "code": 200
}
```
