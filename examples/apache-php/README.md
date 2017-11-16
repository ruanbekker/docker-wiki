## Apache and PHP

### ulsmith/alpine-apache-php7

Big Thubs up to: [ulsmith](https://github.com/ulsmith/alpine-apache-php7)

- [Docker Hub: ulsmith/alpine-apache-php7](https://hub.docker.com/r/ulsmith/alpine-apache-php7/)
- [Github: ulsmith/alpine-apache-php7](https://github.com/ulsmith/alpine-apache-php7)

Supported Environment Variables:

```
APACHE_SERVER_NAME:                 Change server name to match your domain name in httpd.conf
PHP_SHORT_OPEN_TAG:                 Maps to php.ini 'short_open_tag'
PHP_OUTPUT_BUFFERING:               Maps to php.ini 'output_buffering'
PHP_OPEN_BASEDIR:                   Maps to php.ini 'open_basedir'
PHP_MAX_EXECUTION_TIME:             Maps to php.ini 'max_execution_time'
PHP_MAX_INPUT_TIME:                 Maps to php.ini 'max_input_time'
PHP_MAX_INPUT_VARS:                 Maps to php.ini 'max_input_vars'
PHP_MEMORY_LIMIT:                   Maps to php.ini 'memory_limit'
PHP_ERROR_REPORTING:                Maps to php.ini 'error_reporting'
PHP_DISPLAY_ERRORS:                 Maps to php.ini 'display_errors'
PHP_DISPLAY_STARTUP_ERRORS: Maps to php.ini 'display_startup_errors'
PHP_LOG_ERRORS: Maps to php.ini 'log_errors'
PHP_LOG_ERRORS_MAX_LEN: Maps to php.ini 'log_errors_max_len'
PHP_IGNORE_REPEATED_ERRORS: Maps to php.ini 'ignore_repeated_errors'
PHP_REPORT_MEMLEAKS: Maps to php.ini 'report_memleaks'
PHP_HTML_ERRORS: Maps to php.ini 'html_errors'
PHP_ERROR_LOG:                      Maps to php.ini 'error_log'
PHP_POST_MAX_SIZE:                  Maps to php.ini 'post_max_size'
PHP_DEFAULT_MIMETYPE:               Maps to php.ini 'default_mimetype'
PHP_DEFAULT_CHARSET:                Maps to php.ini 'default_charset'
PHP_FILE_UPLOADS:                   Maps to php.ini 'file_uploads'
PHP_UPLOAD_TMP_DIR:                 Maps to php.ini 'upload_tmp_dir'
PHP_UPLOAD_MAX_FILESIZE:            Maps to php.ini 'upload_max_filesize'
PHP_MAX_FILE_UPLOADS:               Maps to php.ini 'max_file_uploads'
PHP_ALLOW_URL_FOPEN:                Maps to php.ini 'allow_url_fopen'
PHP_ALLOW_URL_INCLUDE:              Maps to php.ini 'allow_url_include'
PHP_DEFAULT_SOCKET_TIMEOUT:         Maps to php.ini 'default_socket_timeout'
PHP_DATE_TIMEZONE:                  Maps to php.ini 'date.timezone'
PHP_PDO_MYSQL_CACHE_SIZE:           Maps to php.ini 'pdo_mysql.cache_size'
PHP_PDO_MYSQL_DEFAULT_SOCKET:       Maps to php.ini 'pdo_mysql.default_socket'
PHP_SESSION_SAVE_HANDLER:           Maps to php.ini 'session.save_handler'
PHP_SESSION_SAVE_PATH:              Maps to php.ini 'session.save_path'
PHP_SESSION_USE_STRICT_MODE:        Maps to php.ini 'session.use_strict_mode'
PHP_SESSION_USE_COOKIES:            Maps to php.ini 'session.use_cookies'
PHP_SESSION_COOKIE_SECURE:          Maps to php.ini 'session.cookie_secure'
PHP_SESSION_NAME:                   Maps to php.ini 'session.name'
PHP_SESSION_COOKIE_LIFETIME:        Maps to php.ini 'session.cookie_lifetime'
PHP_SESSION_COOKIE_PATH:            Maps to php.ini 'session.cookie_path'
PHP_SESSION_COOKIE_DOMAIN:          Maps to php.ini 'session.cookie_domain'
PHP_SESSION_COOKIE_HTTPONLY:        Maps to php.ini 'session.cookie_httponly'
```

Example Dockerfile:

```
FROM ulsmith/alpine-apache-php7
MAINTAINER You <you@youremail.com>

ADD /public /app/public
RUN chown -R apache:apache /app
```

Example Compose File:

```
version: "3.3"
services:
  myservice:
    image: ulsmith/alpine-apache-php7
    labels:
      - "traefik.backend=myservice"
      - "traefik.frontend.rule=Host:myservice.docker.localhost"
    environment:
      - MYSQL_HOST=mysql
      - APACHE_SERVER_NAME=myservice.docker.localhost
      - PHP_SHORT_OPEN_TAG=On
      - PHP_ERROR_REPORTING=E_ALL
      - PHP_DISPLAY_ERRORS=On
      - PHP_HTML_ERRORS=On
    networks:
      - default
    volumes:
      - type: bind
        source: /opt/disk/data/mysql
        target: /var/lib
networks:
  default:
    external:
      name: docker_docker-localhost
```
