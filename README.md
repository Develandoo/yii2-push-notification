Yii2 apns/gcm push notification 
=================

### INSTALLATION
Run
```
composer require develandoo/yii2-push-notification
```
or add
```
 "develandoo/yii2-push-notification": "^1.0"
```

### CONFIGURATION

*in your main.php your configuration would look like this*

```php
    'components' => [
         'push' => [
             'class' => 'develandoo\notification\Push',
             'options' => [
                 'returnInvalidTokens' => true //default false
             ],
             'apnsConfig' => [
                 'environment' => Push::APNS_ENVIRONMENT_PRODUCTION or Push::APNS_ENVIRONMENT_SANDBOX,
                 'pem' => 'PEM_FILE_ABS_URL',
                 'passphrase' => 'YOUR_PASS_PHRASE', //optional
             ],
             'gcmConfig' => [
                 'apiAccessKey' => 'YOUR_GCM_API_KEY'
             ]
         ]
     ]
```

### EXAMPLE

```php
$push = Yii::$app->push;

// ios signle token example
$push->ios()->send('token', [
    'custom-key' => 'custom-value',
    'aps' => [
        'alert' => [
            'loc-key' => 'i18n_key',
            'loc-args' => ['arg1'],
        ]
    ],
    'badge' => 1,
    'sound' => 'default'
]);

// ios multiple tokens example
$push->ios()->send(['token1,token2'], [
    'custom-key' => 'custom-value',
    'aps' => [
        'alert' => 'STRING_MESSAGE'
    ],
    'badge' => 1,
    'sound' => 'default'
]);

// android example
$push->android()->send(['token1,token2'], [
    'key' => 'i18n_key',
    'args' => ['arg1'],
    'custom-key'=>'custom-value'
]);

// mixed tokens example
$push->send([
    'ios-tokens1',
    'android-token1',
    'android-token2',
    'ios-token2'
], $payload);
```

### EXCEPTION CASES

- `Apns environment is invalid.`
- `Apns pem is invalid.`
- `Gcm api access key is invalid.`
- `Gcm in not enabled.`
- `Apns in not enabled.`

© [DEVELANDOO](http://develandoo.com) 2017
