---
title: websocket-client
description: PRipple中支持通过\P\Net::WebSocket()方法操作WebSocket, 用于处理WebSocket客户端连接。
keywords: ['PRipple', 'PHP', '协程', '高性能', '高并发', 'WebSocket', 'Net']
---

### 概述

PRipple提供了一个易用的WebSocketClient组件,可以用于创建WebSocket客户端连接。

```php
use P\Net;
use Psc\Library\Net\WebSocket\Client\Connection;
use function P\run;

$connection            = Net::WebSocket()->connect('wss://echo.websocket.org');
$connection->onOpen(function (Connection $connection) {
    $connection->send('{"action":"ping","data":[]}');
});

$connection->onMessage(function (string $data, Connection $connection) {
    echo 'Received: ' . $data . \PHP_EOL;
});

$connection->onClose(function (Connection $connection) {
    echo 'Connection closed' . \PHP_EOL;
});

run();
```


