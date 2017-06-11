# Command Usage

## ssh
\#ssh -l usr -p 22 127.0.0.1

## scp
put file  
\#scp -P 22 ./file usr@127.0.0.1:/home/usr  
  
get file     
\#scp -P 22 usr@127.0.0.1:/home/usr/file ./

## Shadowsocks
run ss in the background  
\#ssserver -c /etc/shadowsocks.json -d start  
or  
\#/usr/bin/python /usr/local/bin/ssserver -c /etc/shadowsocks.json  
  
log file  
/var/log/shadowsocks.log

shadowsocks.json  
```  
{
    "server":"local ip",  
    "server_port":port,  
    "local_address": "127.0.0.1",  
    "local_port":1080,  
    "password":"password",  
    "timeout":300,  
    "method":"aes-256-cfb",  
    "fast_open": false  
}
```
# tcpdump
save data to file, then open the file using wireshark  
\#tcpdump -i any -s 0 -w file.pcap
# kcptun
forwarding port:6666, service port:4000  
\#./kcptun_server -t "127.0.0.1:6666" -l ":4000" -mode fast2  
client local port:8388, server ip:vps  
\#./kcptun_client -r "vps:4000" -l ":8388" -mode fast2
# date
\#date "+%Y.%m.%d %H:%M:%S" --date="+12 hour"
# apache
\#service apache2 start  
\#service apache2 restart  
\#service apache2 status  
# rtorrent
start: 		screen torrent  
back: 		Ctrl+A+D  
restart:	screen -r  

start: Ctrl+s  
quit: Ctrl+q  
delete: Ctrl+d	x2 delete  
# cron 
create cron script file  
\#cd  /var/spool/cron/crontabs  
 #vi mycron   
*/2 * * * * /run.sh

run script    
 #crontab mycron  

list script file  
 #crontab -l

edit script  file  
 #crontab -e

delete script  file  
 #crontab -r
# view netspeed
\#install sysstat  
\#sar -n DEV 1 100
# nginx
conf file  
\#vim /etc/nginx/sites-available/default

start  
\#nginx -c /etc/nginx/nginx.conf

stop  
\#nginx -s stop  
# run in the background
Ctrl+Z  
\#bg 1  
\#jobs  
\#fg 1  

# nfs
\# mount -t nfs -o nolock 192.168.1.100:/nfs /home
