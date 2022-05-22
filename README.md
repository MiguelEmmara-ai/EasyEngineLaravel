# EasyEngineLaravel
How To Install Laravel On EasyEngine

*Note, All the 'example.com' and 'examplecom' must be change to your domain name!

## 1 Install EE
```shell
wget -qO ee rt.cx/ee4 && sudo bash ee
```

## 2 Add Necessary Packages
```shell
apt-get install php8.0-mbstring php8.0-xml php8.0-dom
```
*Might change php version depending on the update

## 3 Install Latest Composer
```shell
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
php -r "if (hash_file('sha384', 'composer-setup.php') === '55ce33d7678c5a611085589f1f3ddf8b3c52d662cd01d4ba75c0ee0459970c2200a51f492d557530c71c15d8dba01eae') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
php composer-setup.php
php -r "unlink('composer-setup.php');"
mv composer.phar /usr/local/bin/composer
mv composer.phar /usr/bin/composer
```

## 4 Add Our Site 
```shell
ee site create example.com --type=php --ssl=le --with-db --php=8.0
```
This command will add "example.com" with database, ssl, and PHP version 8.0

## 5 CD To Our Domain Directory
```shell
cd /var/lib/docker/volumes/examplecom_htdocs/_data/htdocs
```

## 6 Install Laravel
```shell
composer create-project laravel/laravel example-app
```

## 7 Configure Laravel
```shell
chown -R www-data.www-data /var/lib/docker/volumes/examplecom_htdocs/_data/htdocs/lara/storage
chown -R www-data.www-data /var/lib/docker/volumes/examplecom_htdocs/_data/htdocs/lara/bootstrap/cache
```

## 8 Edit Nginx Root Dir
```shell
cd /var/lib/docker/volumes/exampleme_config_nginx/_data/conf.d
nano main.conf

Here we must edit "root /var/www/htdocs;" To "root /var/www/htdocs/example-app/public;"
(example-app) is the laravel app name we created earlier in Step 6
Save
```

## 9 Reload
```shell
ee site reload example.com
```

# Done

You can then proceed building your web app like usual!

You can also edit .env file based on your site info

## 8 Get your site info with
```shell
ee site info example.com
```
