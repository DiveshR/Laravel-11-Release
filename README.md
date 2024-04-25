<p align="center"><a href="https://laravel.com" target="_blank"><img src="https://raw.githubusercontent.com/laravel/art/master/logo-lockup/5%20SVG/2%20CMYK/1%20Full%20Color/laravel-logolockup-cmyk-red.svg" width="400" alt="Laravel Logo"></a></p>

<p align="center">
<a href="https://github.com/laravel/framework/actions"><img src="https://github.com/laravel/framework/workflows/tests/badge.svg" alt="Build Status"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/dt/laravel/framework" alt="Total Downloads"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/v/laravel/framework" alt="Latest Stable Version"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/l/laravel/framework" alt="License"></a>
</p>

#### Laravel 11.x requires a minimum PHP version of 8.2.

##  Laravel 11 New Features

#### New Wow Look Welcome Page.

<img width="1268" alt="Screenshot 2024-03-12 at 8 30 53 PM" src="https://github.com/DiveshR/Laravel-11-Release/assets/25860707/b139135c-a508-417f-a4ea-489a8d52b0f3">

#### New Directory Structure Changes.

##### In Laravel 10 
 ###### app directory
 ```
 Console,Exceptions,Http,Models,Providers Directories
 ```
##### In Laravel 11 
 ###### app directory only
  ```
 Http,Models,Providers Directories
 ```

 ##### In Laravel 10 
 ###### Http  directory
 ```
 Controllers,Middleware Directories & Kernel.php file
 ```
##### In Laravel 11 
 ###### Http directory only have
  ```
 Controllers Directory
 ```

 ##### In Laravel 11 
 ###### app directory only
  ```
 Http,Models,Providers Directories
 ```

 ##### In Laravel 10 
 ###### Config  directory - 16 files
 
##### In Laravel 11  - It remains 10 files

  ```
 broadcasting.php, cors.php,hashing.php,sanctum.php,view.php is removed
 ```
#### Using config artisan publish command to get config file back.
```
php artisan config:publish
```
<img width="881" alt="Screenshot 2024-03-12 at 8 56 49 PM" src="https://github.com/DiveshR/Laravel-11-Release/assets/25860707/e6c02010-4cf2-4d07-812d-e2f56c663739">


##### In Laravel 11  - Now We have only 3 default migrations.
```
0001_01_01_000000_create_users_table.php,0001_01_01_000001_create_cache_table.php,0001_01_01_000002_create_jobs_table.php
```
###### Date timestamps are removed from the database migrations.

 ##### In Laravel 10 
 ###### routes  directory
 ```
 api.php,channels.php,console.php,web.php files
 ```
##### In Laravel 11 - we have only 2 default route files.
 ###### Http directory only have
 ```
 console.php,web.php files
 ```
There is no api.php
 ###### artisan command to generate api route in laravel11
```
php artisan install:api
```
 ###### By running install:api command - It perform following actions.
 - This install api command install sanctum package.
 - Then uncomment line api: __DIR__.'/../routes/api.php', in bootstrap/app.php 
 - Publish sanctum publish file in config directory.
 - Create new migration for personal access tokens(2024_03_12_154117_create_personal_access_tokens_table.php)
 - Create api.php route.


#### Models - casts in Model

 ##### In Laravel 10 - we define as protected cast property.
 ###### app/Models/User.php 
 ```
    /**
     * The attributes that should be cast.
     *
     * @var array<string, string>
     */

    protected $casts = [
        'email_verified_at' => 'datetime',
        'password' => 'hashed',
    ];
 ```
##### In Laravel 11 - we define cast as protected casts() method.

 ```
     /**
     * Get the attributes that should be cast.
     *
     * @return array<string, string>
     */
    protected function casts(): array
    {
        return [
            'email_verified_at' => 'datetime',
            'password' => 'hashed',
        ];
    }
 ```

##### In Laravel 11 - Modifying Columns.
When modifying a column, you must now explicitly include all the modifiers you want to keep on the column definition after it is changed.
For example, imagine you have a migration that creates a votes column with the unsigned, default, and comment attributes:
```
Schema::create('users', function (Blueprint $table) {
    $table->integer('votes')->unsigned()->default(1)->comment('The vote count');
});
```
Later, you write a migration that changes the column to be nullable as well:
```
Schema::table('users', function (Blueprint $table) {
    $table->integer('votes')->nullable()->change();
});
```
In Laravel 10, this migration would retain the unsigned, default, and comment attributes on the column. However, in Laravel 11, the migration must now also include all of the attributes that were previously defined on the column. Otherwise, they will be dropped:
```
Schema::table('users', function (Blueprint $table) {
    $table->integer('votes')
        ->unsigned()
        ->default(1)
        ->comment('The vote count')
        ->nullable()
        ->change();
});
```
