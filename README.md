npefk
====
docker file of nginx + php-fpm + elasticsearch + fluentd + kibana

How to use
----
1. Clone or fork this project.
2. Edit docker-compose.yml, on ```volumes``` block, replace your webroot path at host machine here.
3. Edit nginx.conf for your project.
4. Run ```composer up```

Versions
----
|Image name|Version|
|---|---|
|Nginx|latest|
|PHP-fpm|latest|
|Elasticsearch|6.2.3|
|Fluentd|v0.12-onbuild|
|Kibana|6.2.4|
