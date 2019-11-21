# Docker PHP-FPM 7.3, NGINX 16
This image is based off https://github.com/TrafeX/docker-php-nginx
What's added is opcache extension and enabled it by default.

* Built on the lightweight and secure Alpine Linux distribution
* Very small Docker image size (+/-35MB)
* Uses PHP 7.3 for better performance, lower cpu usage & memory footprint
* Optimized for 100 concurrent users
* Optimized to only use resources when there's traffic (by using PHP-FPM's ondemand PM)
* The servers Nginx, PHP-FPM and supervisord run under a non-privileged user (nobody) to make it more secure
* The logs of all the services are redirected to the output of the Docker container (visible with `docker logs -f <container name>`)
* Follows the KISS principle (Keep It Simple, Stupid) to make it easy to understand and adjust the image to your needs

## Usage

Start the Docker container:

    docker run -p 80:8080 matthewsuan/nginx-php-fpm-opcache

See the PHP info on http://localhost, or the static html page on http://localhost/test.html
Or mount your own code to be served by PHP-FPM & Nginx

    docker run -p 80:8080 -v ~/my-codebase:/var/www/html matthewsuan/nginx-php-fpm-opcache

## Configuration
In [config/](config/) you'll find the default configuration files for Nginx, PHP and PHP-FPM.
If you want to extend or customize that you can do so by mounting a configuration file in the correct folder;

Nginx configuration:

    docker run -v "`pwd`/nginx-server.conf:/etc/nginx/conf.d/server.conf" matthewsuan/nginx-php-fpm-opcache

PHP configuration:

    docker run -v "`pwd`/php-setting.ini:/etc/php7/conf.d/settings.ini" matthewsuan/nginx-php-fpm-opcache

PHP-FPM configuration:

    docker run -v "`pwd`/php-fpm-settings.conf:/etc/php7/php-fpm.d/server.conf" matthewsuan/nginx-php-fpm-opcache

_Note; Because `-v` requires an absolute path I've added `pwd` in the example to return the absolute path to the current directory_ 
