# neteasy-yunxin

---
[网易云信](https://www.163yun.com/help/documents/18132200658681856) 服务端sdk for Laravel5 / Lumen. based on [salamander-mh/YunXinHelper](https://github.com/salamander-mh/YunXinHelper).

## Installation

Require this package with composer by using the following command:

```
$ composer require haibin2017/easy-yunxin
```

Then, add the service provider:

If you are using Laravel, add the service provider to the providers array in `config/app.php`:

```php
[
    'providers' => [
        Woshuo\YunXin\YunXinServiceProvider::class,
    ],
]
```

Laravel 5.5+ 会自动注册服务提供者可过滤

If you are using Lumen, append the following code to `bootstrap/app.php`:

```php
$app->register(Woshuo\YunXin\YunXinServiceProvider::class);
```


## Configuration

The defaults are set in config/yunxin.php. Copy this file to your own config directory to modify the values. You can publish the config using this command:

```php
php artisan vendor:publish --provider="Woshuo\YunXin\YunXinServiceProvider"

```

If you are using Lumen, append the following code to `bootstrap/app.php`:

```php
$app->configure('yunxin');
```

## Usage
### 实例化
```
use Woshuo\YunXin\Entrance;

$appKey = config('yunxin.app_key');
$appSecret = config('yunxin.app_secret');
$helper = new Entrance($appKey, $appSecret);
$user = $helper->user();
$chat = $helper->chat();
```

### 用户
```
# 创建用户
$user->create($accid, $name, $icon);


# 用户基本信息更新
$user->update($accid, $token);


# 封禁用户
$user->block($accid);


# 解禁用户
$user->unblock($accid);


# 更新用户名片
$user->updateUserInfo($accid, $name, $icon);


# 批量获取用户名片
$user->getUserInfos($accids);
```

### 消息功能
```
# 文本消息
$chat->sendTextMsg($accidFrom, $to, $open, $text);

# 图片消息
$chat->sendPictureMsg($accidFrom, $to, $open,
        $picName, $picMD5, $picUrl, $picExt, $picWidth, $picHeight, $picSize);

# 批量文本消息
$chat->sendTextBatchMsg($accidFrom, $accidsTo, $text);


# 发送自定义系统通知
$chat->sendAttachMsg($from, CHAT::CHAT_ONT_TO_ONE, $to, $attach);
```

## License

The package is open-sourced software licensed under the [MIT license](http://opensource.org/licenses/MIT).


