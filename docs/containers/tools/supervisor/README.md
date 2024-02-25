

1. Setup Supervisor Config

`supervisord.conf`
```ini
[supervisord]
nodaemon=true
user=root
logfile=/dev/null
logfile_maxbytes=0

[program:app1]
stdout_logfile=/dev/fd/1
stdout_logfile_maxbytes=0
redirect_stderr=true
directory=/root/app1
command=node app1.js

[program:app2]
stdout_logfile=/dev/fd/1
stdout_logfile_maxbytes=0
redirect_stderr=true
directory=/root/app2
command=node app2.js
```

2. Using Supervisor in Docker

```Dockerfile
RUN apt-get install supervisor
RUN mkdir -p /var/log/supervisor

COPY supervisord.conf /etc/supervisor/supervisord.conf

ENTRYPOINT ["/usr/bin/supervisord", "-c", "/etc/supervisor/supervisord.conf"]
```