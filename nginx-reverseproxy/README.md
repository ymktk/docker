# Reverse proxy nginx sample

```bash
          localhost:8083
                +
                |    location /wp-context/+-----------------+
                |   +-------------------->  www.nginx.com  |
                |   |                    +-----------------+
                v   +                    https://www.nginx.com/wp-content/uploads/2019/05/NGINX-plus-oss-logos_featured.png
          +-------------+
          |   proxy     |
          +-+---------+-+
            |         |
 location / |         | location /2/
            |         |
nginx1      v         v      nginx2
+--------------+    +-------------+
| index.html   |    | index.html  |
+--------------+    +-------------+
                    <img src="/wp-content/uploads/2019/05/NGINX-plus-oss-logos_featured.png">

```