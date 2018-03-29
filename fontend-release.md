# 编译发布

## 后端

```bash

```

## 前端

```bash
>> npm run build

Hash: 9dd56b56e0c0db93c932
Version: webpack 3.11.0
Time: 20979ms
                                                  Asset       Size  Chunks                    Chunk Names
    static/css/app.df68eba4405f15f5b344ec63333ee47f.css     201 kB      11  [emitted]         app
                 static/fonts/element-icons.6f0a763.ttf      11 kB          [emitted]
                             static/img/401.089007e.gif     164 kB          [emitted]
                    static/js/0.a803cb94e0f82ef375a2.js    40.6 kB    0, 3  [emitted]
                    static/js/1.25ac94fd9f91feed1737.js    8.14 kB       1  [emitted]
                    static/js/2.4eaa09e7119ee8c55e90.js    1.93 kB       2  [emitted]
                    static/js/3.af143fe5b62abedb6061.js    2.07 kB       3  [emitted]
                    static/js/4.c64df6ba7177531478a0.js  466 bytes       4  [emitted]
                    static/js/5.1960cd9fcc025628b204.js  480 bytes       5  [emitted]
                    static/js/6.2e89b70de27b932b121a.js  466 bytes       6  [emitted]
                    static/js/7.58bcc8ea9e9aa17db097.js  466 bytes       7  [emitted]
                    static/js/8.6b7e742b185b0a28b5ec.js  531 bytes       8  [emitted]
                    static/js/9.5d4e1b3e668683969958.js  379 bytes       9  [emitted]
               static/js/vendor.7b937696033463974717.js     776 kB      10  [emitted]  [big]  vendor
                  static/js/app.201822aae8242efcdebf.js    89.2 kB      11  [emitted]         app
             static/js/manifest.11660fe906e412e8aaf8.js    1.69 kB      12  [emitted]         manifest
                             static/img/404.a57b6f3.png    98.1 kB          [emitted]
static/css/app.df68eba4405f15f5b344ec63333ee47f.css.map     307 kB          [emitted]
                static/js/0.a803cb94e0f82ef375a2.js.map     156 kB    0, 3  [emitted]
                static/js/1.25ac94fd9f91feed1737.js.map    18.3 kB       1  [emitted]
                static/js/2.4eaa09e7119ee8c55e90.js.map    8.81 kB       2  [emitted]
                static/js/3.af143fe5b62abedb6061.js.map    9.29 kB       3  [emitted]
                static/js/4.c64df6ba7177531478a0.js.map    3.23 kB       4  [emitted]
                static/js/5.1960cd9fcc025628b204.js.map    3.31 kB       5  [emitted]
                static/js/6.2e89b70de27b932b121a.js.map    3.23 kB       6  [emitted]
                static/js/7.58bcc8ea9e9aa17db097.js.map    3.22 kB       7  [emitted]
                static/js/8.6b7e742b185b0a28b5ec.js.map    3.46 kB       8  [emitted]
                static/js/9.5d4e1b3e668683969958.js.map    1.84 kB       9  [emitted]
           static/js/vendor.7b937696033463974717.js.map    3.01 MB      10  [emitted]         vendor
              static/js/app.201822aae8242efcdebf.js.map     227 kB      11  [emitted]         app
         static/js/manifest.11660fe906e412e8aaf8.js.map    8.18 kB      12  [emitted]         manifest
                                             index.html  527 bytes          [emitted]

  Build complete.

  Tip: built files are meant to be served over an HTTP server.
  Opening index.html over file:// won't work.
```

将 `dist` 目录下的文件，直接放到 nginx 服务器上的 web 目录

## `nginx.conf` 配置

```js
server {
    listen 80;
    server_name localhost;

    location / {
        # 指向我们打包后上传的前端文件
        root /opt/nginx/dist;
        index index.html;
    }
    location ^~ /api/ {
        rewrite ^/api/(.*)$ /$1 break;
        proxy_pass http://127.0.0.1:8001/api/;
        proxy_redirect off;
    }
}
```
