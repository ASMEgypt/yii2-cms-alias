Alias module for Yii 2
========================


Installation
------------

The preferred way to install this extension is through [composer](http://getcomposer.org/download/).

Either run

```
php composer.phar require infoweb-internet-solutions/yii2-cms-alias "*"
```

or add

```
"infoweb-internet-solutions/yii2-cms-alias": "*"
```

to the require section of your `composer.json` file.


Usage
-----

Once the extension is installed, simply modify your application configuration as follows:

Your backend configuration as follows:

```php
'modules' => [
    ...
    'alias' => [
        'class' => 'infoweb\alias\Module',
        'reservedUrls' => ['page'] // Url's that are reserved by the application
    ],
],
```

Import the translations and use category 'infoweb/alias':
```
yii i18n/import @infoweb/alias/messages
```

To use the module, execute yii migration
```
yii migrate/up --migrationPath=@vendor/infoweb-internet-solutions/yii2-cms-alias/migrations
```

Behavior
--------
With this behavior you can manage the `url` field for the entity that the `Alias` is attached to.
The `AliasBehavior` has to be attached to an `ActiveRecord` class that has a language identifier.
Below is an example of how it can be attached to `\infoweb\pages\models\Page`

```php
use infoweb\alias\behaviors\AliasBehavior;

public function behaviors()
{
    return [
        'alias' => [
            'class' => AliasBehavior::className(),
            'entityType' => Page::className(),
            'entityIdField' => 'page_id'
        ],
    ];
}
```

The `url` field can be rendered in your `ActiveForm` view

```php
 // Initialize the tabs
<?= $this->render('@infoweb/alias/views/behaviors/alias/_url', [
        'form' => $form,
        'model' => $model,
        'alias' => $alias,
        'readonly' => false,
        'duplicateable' => true,
        'urlPrefix' => ''
    ]) ?>
```