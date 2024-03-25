# 10-2 Стасенко Григорий Домашнее задание к занятию «Кластеризация и балансировка нагрузки» 10-2

## Задание 1

````
listen stats  # веб-страница со статистикой
        bind                    :888
        mode                    tcp
        stats                   enable
        stats uri               /stats
        stats refresh           5s
        stats realm             Haproxy\ Statistics

frontend example  # секция фронтенд
        mode tcp
        bind :8088
        default_backend web_servers

backend web_servers    # секция бэкенд
        mode tcp
        balance roundrobin
        option httpchk
        http-check send meth GET uri /index.html
        server s1 127.0.0.1:8888 check
        server s2 127.0.0.1:9999 check

listen web_tcp

        bind :1325

        server s1 127.0.0.1:8888 check inter 3s
        server s2 127.0.0.1:9999 check inter 3s
````

![image](https://github.com/Nightnek/availiability-10-2/assets/127677631/0e9d116a-f5cc-449f-b14a-08e5592f2f58)



---

## Задание 2

![image](https://github.com/Nightnek/availiability-10-2/assets/127677631/ff003475-686e-48f1-a97c-afe7ebb6f314)


````
listen stats  # веб-страница со статистикой
        bind                    :888
        mode                    http
        stats                   enable
        stats uri               /stats
        stats refresh           5s
        stats realm             Haproxy\ Statistics

frontend example  # секция фронтенд
        mode http
        bind :8088
        #default_backend web_servers
        acl ACL_example.local hdr(host) -i example.local
        use_backend web_servers if ACL_example.local

backend web_servers    # секция бэкенд
        mode http
        balance roundrobin
        option httpchk
        http-check send meth GET uri /index.html
        server s1 127.0.0.1:8888 check weight 2
        server s2 127.0.0.1:9999 check weight 3
        server s3 127.0.0.1:7777 check weight 4
````

---

## Задание 3


---
