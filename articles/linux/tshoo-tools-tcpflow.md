# HEC Tshoot using tcpflow

```code
apt-get install tcpflow
```

Regra
```
tcpflow -c host <ip ou hostname>
```
#REQUEST
```
reportfilename: ./report.xml
tcpflow: listening on enp1s0
XXX.XXX.XXX.XXX.34850-XXX.XXX.XXX.XXX.08088: POST /services/collector/raw HTTP/1.1
Host: XXX.XXX.XXX.XXX:8088
User-Agent: python-requests/2.28.2
Accept-Encoding: gzip, deflate
Accept: */*
Connection: keep-alive
Authorization: xxxxxx <TOKEN XXXXXXXXXXXXXXXXXXXXXXX>
Content-Type: application/json
Content-Encoding: gzip
Content-Length: 1836
```

#RESPONSE
```
XXX.XXX.XXX.XXX.34850-XXX.XXX.XXX.XXX.34812: HTTP/1.1 200 OK
Date: Tue, 14 Mar 2023 15:19:55 GMT
Content-Type: text/html; charset=UTF-8
X-Content-Type-Options: nosniff
X-Content-Type-Options: nosniff
Content-Length: 27
Vary: Authorization
Connection: Keep-Alive
X-Frame-Options: SAMEORIGIN
Server: xxxxxxxx

{"text":"Success","code":0}

```

