# Nginx_with_PHP_42
## How to install PHP on Nginx server at 42.
### First step getting nginx:
  1. Run the following command ```brew update && brew install nginx```. Start nginx ```nginx -s reload``` or ```brew services start nginx```. Try if it work's. Open your Browser http://localhost:8080/

  2. Now you should modify a little bit your nginx configuration. Open **nginx.conf** which should be in _/Users/<student_login>/.brew/etc/nginx/nginx.conf_

  3. Add the following line in first position in **location** in nginx.conf: ```include /Users/<student_login>/.brew/etc/php/7.0/php-fpm.d/php-fpm```.

  4. Now go to /Users/<student_login>/.brew/Cellar/nginx/<nginx_versions (you had just to tab)>/html/. Create a file ```index.php```. And add the following content: ```<?php phpinfo(); ?>```

#### Our nginx is ready to print PHP file, But it's require some more things.

### Second Step getting php-fpm:
  1. Run the following command ```brew tap homebrew/dupes && brew tap homebrew/php && brew install --without-apache --with-fpm --with-mysql php70```
  
  2. Now create a file ```php-fpm``` in _/Users/<student_login>/.brew/etc/php/7.0/php-fpm.d/<create_here>_
  
  3. Add in ```php-fpm``` the following lines: 
```
location ~ \.php$ {
    try_files      $uri = 404;
    fastcgi_pass   127.0.0.1:9000;
    fastcgi_index  index.php;
    fastcgi_param  SCRIPT_FILENAME $document_root$fastcgi_script_name;
    include        fastcgi_params;
}
```

### Final step
Just run ``` nginx -s reload``` you can find the binary in _/Users/<student_login>/.brew/bin/nginx_

Open your Browser http://localhost:8080/
