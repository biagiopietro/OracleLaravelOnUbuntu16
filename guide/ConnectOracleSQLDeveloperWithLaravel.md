[![HitCount](http://hits.dwyl.io/biagiopietro/OracleLaravelOnUbuntu16.svg)](http://hits.dwyl.io/biagiopietro/OracleLaravelOnUbuntu16)
[![GitHub forks](https://img.shields.io/github/forks/biagiopietro/OracleLaravelOnUbuntu16.svg)](https://github.com/biagiopietro/OracleLaravelOnUbuntu16/network)
[![GitHub issues](https://img.shields.io/github/issues/biagiopietro/OracleLaravelOnUbuntu16.svg)](https://github.com/biagiopietro/OracleLaravelOnUbuntu16/issues)
[![GitHub license](https://img.shields.io/github/license/biagiopietro/OracleLaravelOnUbuntu16.svg)](https://github.com/biagiopietro/OracleLaravelOnUbuntu16/blob/master/LICENSE)
---

<h1 align="center">How to connect Oracle SQL Developer with Laravel 5.*</h1>
<p align="center">
<sup>
<b>This guide is for only x64 system. (Tested on Ubuntu 16.04) </b>
</sup>
</p>



## Steps
1) Once Composer has installed or updated your packages you need to register Laravel-OCI8. 
   Open up ```config/app.php``` and find the ```providers``` key and add:
	```
	Yajra\Oci8\Oci8ServiceProvider::class,
	```
2) ```OPTIONAL```
	Finally you can optionally publish a configuration file by running the following Artisan command. 
	If config file is not publish, the package will automatically use what is declared on your ```.env``` file database configuration:
	```
	php artisan vendor:publish --tag=oracle
	```
	This will copy the configuration file to ```config/oracle.php```
	### Note 
	For ```Laravel Lumen``` configuration, make sure you have a ```config/database.php``` file on your project and append the configuration below:
	```
	'oracle' => [
    'driver'        => 'oracle',
    'tns'           => env('DB_TNS', ''),
    'host'          => env('DB_HOST', ''),
    'port'          => env('DB_PORT', '1521'),
    'database'      => env('DB_DATABASE', ''),
    'username'      => env('DB_USERNAME', ''),
    'password'      => env('DB_PASSWORD', ''),
    'charset'       => env('DB_CHARSET', 'AL32UTF8'),
    'prefix'        => env('DB_PREFIX', ''),
    'prefix_schema' => env('DB_SCHEMA_PREFIX', ''),
	],
	```
3) When using oracle, we may encounter a problem on authentication because oracle queries are case sensitive by default. By using this oracle 		user provider, we will now be able to avoid user issues when logging in and doing a forgot password failure because of case sensitive search.
	To use, just update ```auth.php``` config and set the ```driver``` to oracle:
	```
	'providers' => [
		 'users' => [
		     'driver' => 'oracle',
		     'model' => App\User::class,
		 ],
	]
	```
4) See <a href="https://github.com/biagiopietro/OracleLaravelOnUbuntu16/blob/master/example/example.txt">example.txt</a> code to see the Laravel code
5) For more info visit: <a href="https://github.com/yajra/laravel-oci8">laravel-oci8</a>	
6) Move to the Laravel project and type:
    ```
    php artisan migrate
    php artisan serve
	```
7) Finish!!!


## Special Thanks
Special thanks to <a href="https://github.com/puffoCyano">PuffoCyano</a> for his help and <a href="https://stackoverflow.com/">StackOverflow</a> for replies.