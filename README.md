#YAF ported to php to extend portability

[YAF](http://pecl.php.net/package/yaf) is a php framework written in C and available as an extension.

This project is a php equivalent of the C code making your code portable to any server which runs php.
Please note that this project is not intended to be a replacement for the Yaf extension, should consider it
an extension for making your code portable to other servers where the yaf extension is not installed or not possible to
install at the moment....
Yaf C extension installed is aprox. 10 times faster then this Php equivalent....So you should consider making everything possible
to install the C extension.

If you have a php project which is written using YAF and you have no controll on the hosting, or your hosting would not want
to install the YAf extension, then your code will not work.
Using this project the code will work, but of course at much lower speed. At least the portability of your project will increase and can run on most servers (php 5.2 is required).

Diferences:

Instead of 
$app->getDispatcher()->setErrorHandler("error_handler", E_RECOVERABLE_ERROR);
should be used:
$app->getDispatcher()->setErrorHandler("error_handler", E_RECOVERABLE_ERROR|E_USER_ERROR);
as from php E_RECOVERABLE_ERROR cannot be triggered.
Do not use Yaf\ENVIRON use instead \Yaf\Application::app()->environ() or \Yaf\G::iniGet('yaf.environ')


## INSTALL

Copy framework folder into your project folder.
Edit index.php and add this code after APPLICATION_PATH is defined:

if (!extension_loaded('yaf')) {
    //we should load the framework from classes
    include(APPLICATION_PATH . '/framework/loader.php');
}

## BENCHMARK

ab -n 1000 -c 10 http://localhost/work/yaf/testApp/
On my pc yaf php ported is 10 times slower.


## TESTING
- require php >= 5.3 to run the test
- for testing you need to have yaf be loaded as a dynamic extension from command line
- starting php 5.3 dl() cannot be used when php is loaded from modules. Only command line or Fast CGI mode will
  work.
- to run the tests go to /tests/ directory and execute
     - ./runtests.sh - when testing the php framework
     - ./runtests.sh yaf - when testing with yaf.so extension
  

