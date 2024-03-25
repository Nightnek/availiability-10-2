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

![image](https://github.com/Nightnek/availiability-10-2/assets/127677631/e642235e-5e8f-4e68-b919-6f090fc8def4)


---

## Задание 2

 

---

## Задание 3


---
