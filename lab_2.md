#### Вторая часть лабы

[lab2.game-death.ru](lab2.game-death.ru)

Серты минцифры:
```
[root@ct2 ~]# curl -Iv https://ngw.devices.sberbank.ru:9443
* Host ngw.devices.sberbank.ru:9443 was resolved.
* IPv6: (none)
* IPv4: 185.157.96.243
*   Trying 185.157.96.243:9443...
* ALPN: curl offers h2,http/1.1
* TLSv1.3 (OUT), TLS handshake, Client hello (1):
* SSL Trust Anchors:
*   CAfile: /etc/ssl/certs/ca-certificates.crt
* TLSv1.3 (IN), TLS handshake, Server hello (2):
* TLSv1.3 (IN), TLS change cipher, Change cipher spec (1):
* TLSv1.3 (IN), TLS handshake, Encrypted Extensions (8):
* TLSv1.3 (IN), TLS handshake, Request CERT (13):
* TLSv1.3 (IN), TLS handshake, Certificate (11):
* TLSv1.3 (IN), TLS handshake, CERT verify (15):
* TLSv1.3 (IN), TLS handshake, Finished (20):
* TLSv1.3 (OUT), TLS change cipher, Change cipher spec (1):
* TLSv1.3 (OUT), TLS handshake, Certificate (11):
* TLSv1.3 (OUT), TLS handshake, Finished (20):
* SSL connection using TLSv1.3 / TLS_AES_256_GCM_SHA384 / x25519 / RSASSA-PSS
* ALPN: server accepted http/1.1
* Server certificate:
*   subject: CN=ngw.devices.sberbank.ru; O="Sberbank of Russia, Sberbank"; C=RU; ST=77 г.Москва; L=г. Москва; street="117312, ГОРОД МОСКВА, УЛИЦА ВАВИЛОВА, Д. 19"; 1.2.643.100.4=7707083893; OGRN=1027700132195
*   start date: Jun 30 08:02:25 2026 GMT
*   expire date: Jun 30 08:02:25 2027 GMT
*   issuer: C=RU; O=The Ministry of Digital Development and Communications; CN=Russian Trusted Sub CA
*   Certificate level 0: Public key type RSA (2048/112 Bits/secBits), signed using sha256WithRSAEncryption
*   Certificate level 1: Public key type RSA (4096/152 Bits/secBits), signed using sha256WithRSAEncryption
*   subjectAltName: "ngw.devices.sberbank.ru" matches cert's "ngw.devices.sberbank.ru"
* OpenSSL verify result: 0
* SSL certificate verified via OpenSSL.
* Established connection to ngw.devices.sberbank.ru (185.157.96.243 port 9443) from 192.168.1.179 port 39866
* using HTTP/1.x
> HEAD / HTTP/1.1
> Host: ngw.devices.sberbank.ru:9443
> User-Agent: curl/8.21.0
> Accept: */*
>
* Request completely sent off
* TLSv1.3 (IN), TLS handshake, Newsession Ticket (4):
* TLSv1.3 (IN), TLS handshake, Newsession Ticket (4):
< HTTP/1.1 405 Not Allowed
HTTP/1.1 405 Not Allowed
< Server: SynGX
Server: SynGX
< Date: Tue, 15 Sep 2026 09:18:36 GMT
Date: Tue, 15 Sep 2026 09:18:36 GMT
< Content-Type: application/json
Content-Type: application/json
< Content-Length: 46
Content-Length: 46
< Connection: keep-alive
Connection: keep-alive
< Allow: GET, POST
Allow: GET, POST
< Strict-Transport-Security: max-age=31536000; includeSubDomains
Strict-Transport-Security: max-age=31536000; includeSubDomains
<

* Connection #0 to host ngw.devices.sberbank.ru:9443 left intact
```
Токен / ключ:
```
[root@ct2 ~]# ls /etc/caddy/
Caddyfile  conf.d  gigachat  local_llama_cpp
[root@ct2 ~]# cat /etc/caddy/gigachat
header_up Authorization "Bearer eyJjdHkiOiJqd3QiLCJlbmMiOiJBMjU2Q0JDLUhTNTEyIiwiYWxnIjoiUlNBLU9BRVAtMjU2In0.C46Ip9P9pyQW26lFOd2Ag0lQZqroQ97IJ7uJFf-F6JG7axOJftMnnecS3e5du3cV6zwOYTwPwrGCTdrYwONnxi-BdVWBMePwJ7HUSE77_Y5AHJmD4SbQivdU6AOKrJME2aFmyCvBA3cLZfaJyrjnxUQIWVb9wwBdHG5kH-eGV_GkumXaAljjM7Q0-hQWPgrA_xETs4oU5v6p5vdFmOXd9uS5OEBHyg4paBYE1nQoOGLaQUrIyNbfjtm174wo3IBiQOVAtHRY7eemePKV9TqkZFcPrzVQ0hP8s7B2gK5T9-lJkjt7gcsDIWcpaQaeWxLv5-ctEsAqw_49H1v358CFaQ.XIVVzuP1Xb8_MNFxmhDIxg.EkXosjcv0HQDdIlkns5RDDIURHQx8aZT-4jHsNasT3A0D2upSSF-NVqTzVK4YtFPtZ6_EZoj57hbDXGoEiB_Hd29flsxG3rPayW0SXIW9PpfoQzHukPz2zsKAUIV9Tx4YEUsvIMQhfS9aH5kQ2OqkbKMb0AbVPz6fSClPDV0QB8znxFDUm4JKTjKLaak4scQ-hc8AHkiFxHt1sgv-McU90zxE_1lTEsAP9xfUxxOZbWNYpeoGom7vzq6YKWzrzJ0ap_myEh_9l9XXsSKz4k-ETd_M2tYaJnBS9jQBKjEpBB_MCHGyOQWR7deI3u0bUax1p_oVMeA5dlE8R3zMLxHu5QV-nzWTXsMFAz6_HMf7EQ3hL-s5D15qGUFttTzqegyMi6KpJsLpajuvyfxqeCxVKcwhnSv4ZUCV-Ex_asCq5Jc6mu4urvvBoyQwLgni-AdYp2BmbxH-SmotC0Sev674T2sUloLaCZPerK9umzyXt3rnGkSk2HdU66ovN58_BRpyX4rRYzt2T0Ke83EBfLnvuRuiXcMaJKPWy2PUQ7254A3l-45ZZa1uWtqkRuhA3Hvy2KCbY8KRHdAzwn-UkszolkwUryToTSaq21x8IxVjFfZY8_q6ailkDHj50FOZm0K0Y4EF-vA0NDhaAPrgKROaBT7V5crn1hu-HOgzm--uZORuaJdfp3j86dzZ2CiKw3rOMOe7MbbngJSL8Rdr4UZ2r-gHnjscSW7VHTofpCvqfM.eQoOFlLz9T-aYhORYe8dVJDSK926XVFa4F6bAAmu05E"
[root@ct2 ~]# cat /etc/caddy/local_llama_cpp
header_up Authorization "Bearer 327f362f5d1f538941a6ea4ac10a3899eda88de728fe43883355af86dff65846"
```
Скрипт:
```
[root@ct2 ~]# cat /usr/local/bin/token-script-gigachat.sh
#!/bin/bash

set -euo pipefail
caddy_conf_file="/etc/caddy/gigachat"
tmp_file="/tmp/gigachat.tmp"

curl -L -X POST 'https://ngw.devices.sberbank.ru:9443/api/v2/oauth' -H 'Content-Type: application/x-www-form-urlencoded' -H 'Accept: application/json' -H 'RqUID: 9b7c4cfd-6e19-4586-8fd2-875c8402c702' -H "Authorization: Basic $AUTH_KEY" --data-urlencode 'scope=GIGACHAT_API_PERS' -o $tmp_file

TOKEN=$(jq -r '.access_token' "${tmp_file}")

if [[ -z "${TOKEN}" || "${TOKEN}" == "null" ]]; then
    echo "Failed to obtain token" >&2
    rm -f "${tmp_file}"
    exit 1
fi
echo "header_up Authorization \"Bearer ${TOKEN}\"" > $caddy_conf_file
rm -f "${tmp_file}"
systemctl reload caddy
```
systemd:
```
[root@ct2 ~]# cat /etc/systemd/system/get-token-gigachat.service
[Unit]
After=network-online.target
Wants=network-online.target

[Service]
Type=oneshot
EnvironmentFile=/etc/secrets/gigachat.key
ExecStart=/usr/local/bin/token-script-gigachat.sh
[root@ct2 ~]# cat /etc/systemd/system/get-token-gigachat.timer
[Unit]
Description=run get-token-gigachat.service 2s after boot and every 20 minutes

[Timer]
OnBootSec=2s
OnUnitActiveSec=20min
Unit=get-token-gigachat.service

[Install]
WantedBy=timers.target
```
```
[root@ct2 ~]# systemctl status get-token-gigachat
○ get-token-gigachat.service
     Loaded: loaded (/etc/systemd/system/get-token-gig
achat.service; static)
     Active: inactive (dead) since Tue 2026-09-15 09:17:35 UTC; 2min 46s ago
 Invocation: d0feff5c93c14219939801cf0850abdc
TriggeredBy: ● get-token-gigachat.timer
    Process: 160339 ExecStart=/usr/local/bin/token-script-gigachat.sh (code=exited, status=0/SUCCESS)
   Main PID: 160339 (code=exited, status=0/SUCCESS)
   Mem peak: 3.8M
        CPU: 47ms

Sep 15 09:17:35 ct2 systemd[1]: Starting get-token-gigachat.service...
Sep 15 09:17:35 ct2 token-script-gigachat.sh[160340]:   % Total    % Received % Xferd  Average Speed  Time    Time
   Time   Current
Sep 15 09:17:35 ct2 token-script-gigachat.sh[160340]:                                  Dload  Upload  Total   Spent
   Left   Speed
Sep 15 09:17:35 ct2 token-script-gigachat.sh[160340]: [312B blob data]
Sep 15 09:17:35 ct2 systemd[1]: get-token-gigachat.service: Deactivated successfully.
Sep 15 09:17:35 ct2 systemd[1]: Finished get-token-gigachat.service.
```
```
[root@ct2 ~]# systemctl list-timers
NEXT                         LEFT LAST                              PASSED
 UNIT                             ACTIVATES
Tue 2026-09-15 09:37:35 UTC 15min Tue 2026-09-15 09:17:35 UTC 4min 26s ago get-token-gigachat.timer         get-tok
en-gigachat.service
Tue 2026-09-15 21:33:05 UTC   12h Mon 2026-09-14 21:33:05 UTC      11h ago systemd-tmpfiles-clean.timer     systemd
-tmpfiles-clean.service
Wed 2026-09-16 00:00:00 UTC   14h Tue 2026-09-15 00:00:18 UTC       9h ago shadow.timer                     shadow.
service
-                               - Tue 2026-09-15 08:58:15 UTC    23min ago archlinux-keyring-wkd-sync.timer archlin
ux-keyring-wkd-sync.service

4 timers listed.
Pass --all to see loaded but inactive timers, too.
```
Конфиг:
```
[root@ct2 ~]# cat /etc/caddy/conf.d/lab2
lab2.game-death.ru {
    handle {
        root * /srv/http
        try_files {path} /lab2.html
        file_server
    }

    handle_path /gigachat/* {
        reverse_proxy https://api.giga.chat {
            header_up Host api.giga.chat
            import /etc/caddy/gigachat

            flush_interval -1

            transport http {
                response_header_timeout 600s
                read_timeout 600s
            }
        }
    }

    handle_path /local/* {
        reverse_proxy localhost:8089 {
            import /etc/caddy/local_llama_cpp

            flush_interval -1

            transport http {
                response_header_timeout 600s
                read_timeout 600s
            }
        }
    }
    log {
        output file /var/log/caddy/lab2.game-death.ru.access.log
        format json
    }
}
```
Скрины
![](2026-09-15_12-16.png)
![](2026-09-15_12-18.png)