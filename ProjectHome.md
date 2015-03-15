Yaf is a PHP framework similar to zend framework, which is written in c and built as PHP extension



# Yaf has been moved to PECL #
> http://pecl.php.net/package/yaf

# Yaf's Codes are host on Github now #

> https://github.com/laruence/php-yaf

# Introduction #

Yaf是一个用PHP扩展形式提供的PHP开发框架, 相比于一般的PHP框架, 它更快.
它提供了Bootstrap, 路由, 分发, 视图, 插件, 是个一个全功能的PHP框架.

you can refer to [Manual](http://yaf.laruence.com/manual) for more informations.

# 1 Install #
## Compile Yaf in Linux ##
```
$/path/to/phpize
$./configure --with-php-config=/path/to/php-config/
$make && make install
```

# 2 Tutorial #
==layout==:
A classic Application directory layout:
```
- index.php //入口文件
- .htaccess //重写规则    
+ conf
  |- application.ini //配置文件   
- application/
  - Bootstrap.php   //入口启动文件
  + controllers
     - Index.php //默认控制器
  + views    
     |+ index   //控制器
        - index.phtml //默认视图
  + modules //其他模块
  - library
  - models  //model目录
  - plugins //插件目录
```

## index.php ##
index.php in the top directory is the only way in of the application, you should rewrite all request to it(you can use .htaccess in Apache+php\_mod)
```
<?php
define("APP_PATH",  dirname(__FILE__));

$app  = new Yaf_Application(APP_PATH . "/conf/application.ini");
$app->bootstrap() //call bootstrap methods defined in Bootstrap.php
 ->run();
```

## rewrite rules ##
### Apache ###
```
#.htaccess, 当然也可以写在httpd.conf
RewriteEngine On
RewriteCond %{REQUEST_FILENAME} !-f
RewriteRule .* index.php
```

### Nginx ###
```
server {
  listen ****;
  server_name  domain.com;
  root   document_root;
  index  index.php index.html index.htm;

  if (!-e $request_filename) {
    rewrite ^/(.*)  /index.php/$1 last;
  }
}
```

### Lighttpd ###
```
$HTTP["host"] =~ "(www.)?domain.com$" {
  url.rewrite = (
     "^/(.+)/?$"  => "/index.php/$1",
  )
}
```


## application.ini ##
application.ini is the application config file
```
[product]
;支持直接写PHP中的已定义常量
application.directory=APP_PATH "/application/" 
```

## default controller ##
In Yaf, the default controller is named IndexController:
```
<?php
class IndexController extends Yaf_Controller_Abstract {
   public function indexAction() {//默认Action
   }
}
?>
```

## view script ##
The view script for default controller and default action is in the application/views/index/index.phtml, Yaf provides a simple view engineer called Yaf\_View\_Simple, which supported the view template written by PHP.

```
<html>
 <head>
   <title>Hello World</title>
 </head>
 <body>
    Hellow World!
 </body>
</htlm>
```

## Run the Applicatioin ##
```
http://www.yourhostname.com/application/index.php
```

# 3 Classes #
it provide following Classes

| **NAME**  | **COMMENT** |
|:----------|:------------|
| Yaf\_Application |  |
| Yaf\_Dispatcher  |  |
| Yaf\_Bootstrap\_Abstract |  |
| Yaf\_Plugin\_Abstract |  |
| Yaf\_Router |  |
| Yaf\_Route\_Static |  |
| Yaf\_Route\_Simple |  |
| Yaf\_Route\_Supervar |  |
| Yaf\_Route\_Rewrite |  |
| Yaf\_Route\_Regex |  |
| Yaf\_Route\_Map |  |
| Yaf\_Config\_Ini |  |
| Yaf\_Config\_Simple |  |
| Yaf\_Controller\_Abstract |  |
| Yaf\_Action\_Abstract |  |
| Yaf\_Request\_Http |  |
| Yaf\_Request\_Simple |  |
| Yaf\_Exception |  |
| Yaf\_Exception**|**|
| Yaf\_View\_Simple; |  |
| Yaf\_Response\_Abstract |  |
| Yaf\_Response\_Simple |  |
| Yaf\_Response\_Http |  |