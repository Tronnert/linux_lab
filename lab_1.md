#### Первая часть лабы

[lab.game-death.ru](lab.game-death.ru)

curl:
```
[dm_golovanov@kvadra ~]$ curl https://lab.game-death.ru
<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <title>lab</title>
</head>
<body>
    <p>Голованов Дмитрий Игоревич</p>
    <p>host: lab.game-death.ru</p>
    <p>date: 2026-09-14 11:26:33</p>
</body>
</html>
[dm_golovanov@kvadra ~]$ curl http://ct2.lan.com:8081
<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <title>lab</title>
</head>
<body>
    <p>Голованов Дмитрий Игоревич</p>
    <p>host: ct2.lan.com</p>
    <p>date: 2026-09-14 11:26:35</p>
</body>
</html>
```
Конфиг:
```
[root@ct2 ~]# cat /etc/caddy/conf.d/lab
http://:8081 {
   templates
   root * /srv/http
   file_server
   try_files {path} /lab.html
   log {
        output file /var/log/caddy/8081.access.log
        format json
    }
}

https://lab.game-death.ru {
   reverse_proxy http://localhost:8081
   log {
        output file /var/log/caddy/lab.game-death.ru.access.log
        format json
    }
}
```
Прослушиваемые порты:
```
[root@ct2 ~]# ss -tulpn | grep -E "8081|443"
udp   UNCONN 0      0                  *:443              *:*    users:(("caddy",pid=82110,fd=9))
tcp   LISTEN 0      128                *:443              *:*    users:(("caddy",pid=82110,fd=10))
tcp   LISTEN 0      128                *:8081             *:*    users:(("caddy",pid=82110,fd=15))
```
Сертификат:
```
[root@ct2 ~]# openssl x509 -in /var/lib/caddy/certificates/acme-v02.api.letsencrypt.org-directory/lab.game-death.ru/lab.game-death.ru.crt -noout -subject -issuer -dates -ext subjectAltName
subject=CN=lab.game-death.ru
issuer=C=US, O=Let's Encrypt, CN=YE1
notBefore=Sep 14 07:33:55 2026 GMT
notAfter=Dec 13 07:33:54 2026 GMT
X509v3 Subject Alternative Name:
    DNS:lab.game-death.ru
[root@ct2 ~]# cat /var/lib/caddy/certificates/acme-v02.api.letsencrypt.org-directory/lab.game-death.ru/lab.game-death.ru.key
-----BEGIN EC PRIVATE KEY-----
MHcCAQEEIMOaRe7IJhtyFH5UxNo1obuWGH4qA0NisX7cmWW5lck2oAoGCCqGSM49
AwEHoUQDQgAEY3ma7b2pXeipu2mgv8H5/S9lDC1qSIXIEvjUMxB+SjEHmoyoE4WU
0jUd+ZmJHRYFu3AUEuJWoszcqHgrY4TriA==
-----END EC PRIVATE KEY-----
```
Логи:
```
[root@ct2 ~]# cat /var/log/caddy/8081.access.log
{"level":"info","ts":1789385193.0567472,"logger":"http.log.access.log0","msg":"handled request","request":{"remote_ip":"::1","remote_port":"39008","client_ip":"::1","proto":"HTTP/1.1","method":"GET","host":"lab.game-death.ru","uri":"/","headers":{"X-Forwarded-Proto":["https"],"Accept-Encoding":["gzip"],"User-Agent":["curl/8.22.0"],"Accept":["*/*"],"Via":["2.0 Caddy"],"X-Forwarded-For":["185.53.20.219"],"X-Forwarded-Host":["lab.game-death.ru"]}},"bytes_read":0,"user_id":"","duration":0.000498215,"size":255,"status":200,"resp_headers":{"Server":["Caddy"],"Vary":["Accept-Encoding"],"Content-Type":["text/html; charset=utf-8"],"Content-Length":["255"]}}
{"level":"info","ts":1789385195.1059813,"logger":"http.log.access.log0","msg":"handled request","request":{"remote_ip":"192.168.9.2","remote_port":"43226","client_ip":"192.168.9.2","proto":"HTTP/1.1","method":"GET","host":"ct2.lan.com:8081","uri":"/","headers":{"User-Agent":["curl/8.22.0"],"Accept":["*/*"]}},"bytes_read":0,"user_id":"","duration":0.000476781,"size":249,"status":200,"resp_headers":{"Content-Type":["text/html; charset=utf-8"],"Content-Length":["249"],"Server":["Caddy"],"Vary":["Accept-Encoding"]}}
{"level":"info","ts":1789385266.395382,"logger":"http.log.access.log0","msg":"handled request","request":{"remote_ip":"::1","remote_port":"39008","client_ip":"::1","proto":"HTTP/1.1","method":"GET","host":"lab.game-death.ru","uri":"/","headers":{"Accept-Language":["en-US,en;q=0.9"],"X-Forwarded-Proto":["https"],"Sec-Fetch-User":["?1"],"Accept":["text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8"],"User-Agent":["Mozilla/5.0 (X11; Linux x86_64; rv:155.0) Gecko/20100101 Firefox/155.0"],"X-Forwarded-For":["185.53.20.219"],"Priority":["u=0, i"],"Sec-Fetch-Mode":["navigate"],"Upgrade-Insecure-Requests":["1"],"Sec-Fetch-Site":["none"],"X-Forwarded-Host":["lab.game-death.ru"],"Sec-Fetch-Dest":["document"],"Alt-Used":["lab.game-death.ru"],"Accept-Encoding":["gzip, deflate, br, zstd"],"Via":["3.0 Caddy"]}},"bytes_read":0,"user_id":"","duration":0.000443975,"size":255,"status":200,"resp_headers":{"Vary":["Accept-Encoding"],"Content-Type":["text/html; charset=utf-8"],"Content-Length":["255"],"Server":["Caddy"]}}
```
```
[root@ct2 ~]# cat /var/log/caddy/lab.game-death.ru.access.log
{"level":"info","ts":1789385193.057915,"logger":"http.log.access.log1","msg":"handled request","request":{"remote_ip":"185.53.20.219","remote_port":"41564","client_ip":"185.53.20.219","proto":"HTTP/2.0","method":"GET","host":"lab.game-death.ru","uri":"/","headers":{"User-Agent":["curl/8.22.0"],"Accept":["*/*"]},"tls":{"resumed":false,"version":772,"cipher_suite":4865,"proto":"h2","server_name":"lab.game-death.ru","ech":false}},"bytes_read":0,"user_id":"","duration":0.002916602,"size":255,"status":200,"resp_headers":{"Vary":["Accept-Encoding"],"Date":["Mon, 14 Sep 2026 11:26:33 GMT"],"Content-Length":["255"],"Via":["1.1 Caddy"],"Alt-Svc":["h3=\":443\"; ma=2592000"],"Content-Type":["text/html; charset=utf-8"],"Server":["Caddy"]}}
{"level":"info","ts":1789385266.395619,"logger":"http.log.access.log1","msg":"handled request","request":{"remote_ip":"185.53.20.219","remote_port":"45772","client_ip":"185.53.20.219","proto":"HTTP/3.0","method":"GET","host":"lab.game-death.ru","uri":"/","headers":{"Sec-Fetch-Site":["none"],"Alt-Used":["lab.game-death.ru"],"Upgrade-Insecure-Requests":["1"],"Sec-Fetch-Mode":["navigate"],"Sec-Fetch-User":["?1"],"Priority":["u=0, i"],"Accept":["text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8"],"Sec-Fetch-Dest":["document"],"User-Agent":["Mozilla/5.0 (X11; Linux x86_64; rv:155.0) Gecko/20100101 Firefox/155.0"],"Accept-Language":["en-US,en;q=0.9"],"Accept-Encoding":["gzip, deflate, br, zstd"]},"tls":{"resumed":true,"version":772,"cipher_suite":4865,"proto":"h3","server_name":"lab.game-death.ru","ech":false}},"bytes_read":0,"user_id":"","duration":0.000999743,"size":255,"status":200,"resp_headers":{"Vary":["Accept-Encoding"],"Date":["Mon, 14 Sep 2026 11:27:46 GMT"],"Via":["1.1 Caddy"],"Content-Length":["255"],"Content-Type":["text/html; charset=utf-8"],"Server":["Caddy"]}}
```
Скрин
![](2026-09-14_14-36.png)