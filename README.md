# EasyEngineLaravel
How To Install Laravel On EasyEngine

There is not a lot of tutorial on how to setup/install laravel app on a server running EasyEngine
<br>
So here I made one :)

*Side Note, All the 'example.com' and 'examplecom' must be change to your domain name!

## 1 Install EE
```shell
wget -qO ee rt.cx/ee4 && sudo bash ee
```

## 2 Add Our Site 
```shell
ee site create example.com --type=php --ssl=le --with-db --php=8.0
```
This command will add "example.com" with database, ssl, and PHP version 8.0
<br>
Don't forget save the site info once the site created

## 3 Enter Shell
```shell
ee shell example.com --user=root
```
*We need to enter shell to run wp-cli, composer etc.
<br>
We will be in the shell from step 4 -> 8

## 4 Install Laravel #Do This Once
```shell
composer global require laravel/installer << Just Do This Once When We Fresh Install EasyEngine, Don't Run For Your Second Or More Project!, Go Straight To step 6
```
*Just Do This Once When We Fresh Install EasyEngine
<br>
Don't Run For Your Second Or More Project! You Can Go Straight To step 6

## 5 Configure $PATH for composer
```shell
vim ~/.bash_profile 
export PATH=~/.composer/vendor/bin:$PATH << Paste This
source ~/.bash_profile
```
*Just Do This Once When We Fresh Install Laravel

## 6 Add Laravel App
```shell
laravel new example-app
cd example-app
```
*This will Install Laravel App Called "example-app"

## 7 Configure .env
```shell
vim .env
```
Here we must configure our .env file
<br>
All the required data you can get from running ```shell ee site info example.com```

```env
APP_URL=https://example.com

...

DB_CONNECTION=mysql
DB_HOST=global-db
DB_PORT=3306
DB_DATABASE=example_com
DB_USERNAME=example.com-QWERTY
DB_PASSWORD=qafNkpWoCUg0
```

## 8 Migrate Database
```shell
php artisan migrate:fresh
exit
```
We Exit Shell After Migrate

## 9 Edit Nginx Root Dir
Make sure we exit from the shell
```shell
cd /var/lib/docker/volumes/exampleme_config_nginx/_data/conf.d
nano main.conf

Here we must edit "root /var/www/htdocs;" To "root /var/www/htdocs/example-app/public;"
(example-app) is the laravel app name we created earlier in Step 6
Save The File
```

## 10 Chown
```shell
chown -R www-data.www-data /var/lib/docker/volumes/eelaramiguelemmarame_htdocs/_data/htdocs/example-app/storage
chown -R www-data.www-data /var/lib/docker/volumes/eelaramiguelemmarame_htdocs/_data/htdocs/example-app/bootstrap/cache
```

## 11 Reload
```shell
ee site reload example.com
```

# Done

You can then proceed building your web app like usual!
