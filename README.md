Resource Manager component for Yii 2
====================================

[![Latest Stable Version](https://poser.pugx.org/icgarzon/yii2-resource-component/v/stable.svg)](https://packagist.org/packages/Possibility-Companyyii2-ckeditor-widget) [![Total Downloads](https://poser.pugx.org/icgarzon/yii2-resource-component/downloads.svg)](https://packagist.org/packages/icgarzon/yii2-resource-component) [![Latest Unstable Version](https://poser.pugx.org/icgarzon/yii2-resource-component/v/unstable.svg)](https://packagist.org/packages/icgarzon/yii2-resource-component) [![License](https://poser.pugx.org/icgarzon/yii2-resource-component/license.svg)](https://packagist.org/packages/icgarzon/yii2-resource-component)

This extension allows you to manage resources. Currently supports two possible scenarios: 

- Resources to save/or saved on a server's folder
- Resources to save/or saved on an Amazon S3 bucket



Installation
------------

The preferred way to install this extension is through [composer](http://getcomposer.org/download/).

Either run

```sh
php composer.phar require icgarzon/yii2-resource-component "*"
```

or add

```json
"icgarzon/yii2-resource-component": "*"
```

to the require section of your `composer.json` file.

Configuring
--------------------------

Configure the selected component on your configuration file as follows:

```
// For this example we using AmazonS3ResourceManager component
// ...
'components' => [  
	// ...   
	'resourceManager' => [
	'class' => 'possibility-company\resourcemanager\AmazonS3ResourceManager',
		'key' => 'YOUR-AWS-KEY-HERE',
		'secret' => 'YOUR-AWS-SECRET-HERE',
		'bucket' => 'YOUR-AWS-BUCKET-NAME-HERE',
		'region'  => 'YOUR-AWS-BUCKET-REGION-HERE',
	]
	// ...
]
// ...  
```

Done... Now, to save a resource to AWS S3 server, we just need to do the following:

```
// Defensive code checks not written for the example
$resource = yii\web\UploadedFile::getInstanceByName('instance-name');
$name = md5($resource->name) . '.' . $resource->getExtension();
if(\Yii::$app->resourceManager->save($resource, $name)) {
    echo 'Done...';
}