---
title: 手动集成 - Professional
---

### 概述

如果你已经熟悉了PRipple的基本概念和使用方法，那么你可能会想要了解PRipple的更多细节，或者想要对PRipple进行一些定制化的配置。
这时候，你可以通过手动构建PRipple来实现这些目的。该文档将以Laravel为例，介绍如何手动集成PRipple。

### 安装依赖

```php
composer require cclilshy/p-ripple-core
```

### Laravel集成

> 修改入口文件 `index.php`

```php
<?php

use Illuminate\Http\Request;

define('LARAVEL_START', microtime(true));

// Determine if the application is in maintenance mode...
if (file_exists($maintenance = __DIR__.'/../storage/framework/maintenance.php')) {
    require $maintenance;
}

// Register the Composer autoloader...
require __DIR__.'/../vendor/autoload.php';

\P\async(function(){
    // Bootstrap Laravel and handle the request...
    (require_once __DIR__.'/../bootstrap/app.php')
        ->handleRequest(Request::capture());
});

\P\tick();
```

> 上述例子中我们将Laravel的启动过程包含在了PRipple的协程上下文中,并在最后调用了`\P\tick()`函数来处理Laravel运行过程中触发的所有异步事件
> 通过该方法即可为Laravel添加PRipple的异步支持,并能够完美在FPM/CGI模式下运行,
>
> 在此环境下开发的应用,可以在需要时兼容性地以PRipple服务模式运行达到性能质的飞跃