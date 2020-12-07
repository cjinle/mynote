# composer使用国内镜像加速

## 镜像用法

有两种方式启用本镜像服务：

 - 系统全局配置：即将配置信息添加到 Composer 的全局配置文件 config.json 中。见“方法一”
 - 单个项目配置：将配置信息添加到某个项目的 composer.json 文件中。


### 方法一： 修改 composer 的全局配置文件（推荐方式）

打开命令行窗口（windows用户）或控制台（Linux、Mac 用户）并执行如下命令：

```sh
composer config -g repo.packagist composer https://packagist.phpcomposer.com
```



### 方法二： 修改当前项目的 composer.json 配置文件：

打开命令行窗口（windows用户）或控制台（Linux、Mac 用户），进入你的项目的根目录（也就是 composer.json 文件所在目录），执行如下命令：

```sh
composer config repo.packagist composer https://packagist.phpcomposer.com
```

上述命令将会在当前项目中的 	composer.json	 文件的末尾自动添加镜像的配置信息（你也可以自己手工添加）：

```json
"repositories": {
    "packagist": {
        "type": "composer",
        "url": "https://packagist.phpcomposer.com"
    }
}
```

以 thinkphp 项目的 composer.json 配置文件为例，执行上述命令后如下所示（注意最后几行）：

```js
{
    "name": "topthink/think",
    "description": "the new thinkphp framework",
    "type": "project",
    "keywords": [
        "framework",
        "thinkphp",
        "ORM"
    ],
    "homepage": "http://thinkphp.cn/",
    "license": "Apache-2.0",
    "authors": [
        {
            "name": "liu21st",
            "email": "liu21st@gmail.com"
        }
    ],
    "require": {
        "php": ">=5.4.0",
        "topthink/framework": "5.0.15",
        "phpoffice/phpspreadsheet": "1.1.0"
    },
    "extra": {
        "think-path": "thinkphp"
    },
    "config": {
        "preferred-install": "dist"
    },
    "repositories": {
        "packagist": {
            "type": "composer",
            "url": "https://packagist.phpcomposer.com"
        }
    }
}

```