# From apache2.4 alpine
FROM httpd:2.4-alpine

#Update alpine
RUN apk update; \
    apk upgrade;

# Copy sites certificates
COPY ./sites_certificates/local_public_cert/site.local.crt /usr/local/apache2/conf/server.crt
COPY ./sites_certificates/local_public_cert/site.local.key /usr/local/apache2/conf/server.key

#Change the configuration to support ssl and fpm
RUN sed -i \
        -e 's/^#\(Include .*httpd-ssl.conf\)/\1/' \
        -e 's/^#\(LoadModule .*mod_ssl.so\)/\1/' \
        -e 's/^#\(LoadModule .*mod_socache_shmcb.so\)/\1/' \
        -e 's/^#\(Include .*mod_deflate.so\)/\1/' \
        -e 's/^#\(LoadModule .*mod_proxy.so\)/\1/' \
        -e 's/^#\(LoadModule .*mod_proxy_fcgi.so\)/\1/' \
        conf/httpd.conf

# Copy apache vhost file to proxy php requests to php-fpm container
COPY ./sites-available/mage234.local.conf /usr/local/apache2/conf/mage234.local.conf
RUN echo "Include /usr/local/apache2/conf/mage234.local.conf" \
    >> /usr/local/apache2/conf/httpd.conf
