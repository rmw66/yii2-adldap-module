# yii2-adldap-module

[Yii2](http://www.yiiframework.com) extension for adLDAP (https://packagist.org/packages/adldap2/adldap2)

[![Latest Stable Version](https://poser.pugx.org/edvlerblog/yii2-adldap-module/v/stable)](https://packagist.org/packages/edvlerblog/yii2-adldap-module)
[![Total Downloads](https://poser.pugx.org/edvlerblog/yii2-adldap-module/downloads)](https://packagist.org/packages/edvlerblog/yii2-adldap-module)
[![Monthly Downloads](https://poser.pugx.org/edvlerblog/yii2-adldap-module/d/monthly)](https://packagist.org/packages/edvlerblog/yii2-adldap-module)

## Installation


### Composer

The preferred way to install this extension is through [Composer](http://getcomposer.org/).

Either run

	php composer.phar require edvlerblog/yii2-adldap-module "v1.1.0"

or add

	"edvlerblog/yii2-adldap-module": "v1.1.0"

to the require section of your composer.json


## Configuration

Add this code in your components section of the application configuration (eg. config/main.php):

	'components' => [
		..... 
		
		'ldap' => [
			'class'=>'Edvlerblog\Ldap',
			'options'=> [
					'ad_port'      => 389,
					'domain_controllers'    => array('AdServerName1','AdServerName2'),
					'account_suffix' =>  '@test.lan',
					'base_dn' => "DC=test,DC=lan",
					// for basic functionality this could be a standard, non privileged domain user (required)
					'admin_username' => 'ActiveDirectoryUser',
					'admin_password' => 'StrongPassword'
				],
			//Connect on Adldap instance creation (default). If you don't want to set password via main.php you can
			//set autoConnect => false and set the admin_username and admin_password with
			//Yii::$app->ldap->setAdminUsername and Yii::$app->ldap->setAdminPassword function
			//After setting you can connect with Yii::$app->ldap->connect();
			//See http://adldap.sourceforge.net/wiki/doku.php?id=documentation_connections at the bottom
			'autoConnect' => true
		]
		
		...
	]
	
[More abount config options](https://github.com/Adldap2/Adldap2/blob/v5.2/docs/CONFIGURATION.md)


## Examples

To use the yii2-adldap-module you need only one line. 
You can use the yii2-adldap-module everywhere where \Yii::$app works (Controllers, Widgets,...).

Authenticate User:

    $authUser = \Yii::$app->ldap->authenticate("username","password", true);
	var_dump ($authUser);

Group membership of a User:

	$groups = \Yii::$app->ldap->user()->groups("username");
	var_dump($groups);  
	
Get informations about a Group:

	$groupinfo= \Yii::$app->ldap->group()->info("example_group");
	var_dump($groupinfo);  

....
	
[More examples](https://github.com/adldap/adLDAP/blob/master/examples/examples.php)


## DOCUMENTATION
yii2-adldap-module is only a wrapper class. Feel free to learn more about the underlying adLDAP.

You can find the website at https://github.com/adldap2/adLDAP2/
