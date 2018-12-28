npefk
====
docker file of nginx + php-fpm + elasticsearch + fluentd + kibana

How to use
----
1. Clone or fork this project.
2. Edit docker-compose.yml, on ```volumes``` block, replace to your webroot path at host machine here.
3. Edit nginx.conf for your project.
4. Run ```docker-compose up```

Versions
----
|Image name|Version|
|---|---|
|Nginx|latest|
|PHP-fpm|latest|
|Elasticsearch|6.2.3|
|Fluentd|v0.12-onbuild|
|Kibana|6.2.4|
|XDebug|2.6.0RC2|

Extra
----
The default time zone setting is ```Shanghai/Asia```(GMT+8), you can modify the time zone at ```Dockerfile```.

Fluentd listen on port 24224 and forward all logs request to elasticsearch, customize file fluentd/fluentd.conf to matching your log format.

Run ```docker-compose restart nginx``` can reload nginx.conf eaisily, but the configure file of fluentd and kibana was already copied to docker image, run ```docker-compose build fluentd``` to rebuild the image.

The first time start up the container, kibana would cost more than 1.5G memory to build the nodejs serverce, ensure more than 2G memory on your host machine, and you may wait about ten minutes.

Change Log
----
2018.12.28 - Add XDebug for php, remote port: 9004
