+++
author = "roiwk"
title = "php的SSE客户端"
description = "php的SSE客户端"
date = "2023-09-04"
keywords = [
    "sse client",
    "php sse client"
]
tags = [
    "php",
    "sse",
    "composer",
]
categories = [
    "php",
]
draft = false
+++


<p>
 <a href="https://github.com/roiwk/sse-client">
    <img src="https://img.shields.io/badge/roiwk/seeClient-181717?logo=github" alt="github" title="roiwk/sseClient"/>
  </a>
</p>

![Packagist Downloads](https://img.shields.io/packagist/dt/roiwk/sse-client)


# sse-client  SSE客户端
Server Sent Event client  
php的SSE客户端, 采用原生stream,不依赖任何第三方库. 

# 项目缘由:
  php的SSE服务端很容易就能找到, 这里想做一个SSE的客户端(项目需要),要求用起来方便, 类似javascript客户端, 就有了此项目

# Install 安装

```sh
composer require roiwk/sse-client
```

# Usage 使用

## Client  客户端

```php

include 'path/to/autoload.php';

$client = new Roiwk\SSEClient\Client('http://127.0.0.1:8888');
$client->addEventListener('ping', function ($data) {
    echo "Received ping event: $data\n";
});
$client->start();
```


## Server (demo)  服务端

You can use a test server to facilitate the use of this demo client, or use another server. Here is a demo:  
你可以使用一个测试服务器,以方便使用此演示客户端,或着使用别的服务端:  

```php
//server.php
header('Cache-Control: no-store');
header('Content-Type: text/event-stream');

$counter = rand(1, 10);
while (true) {
    // Every second, send a "ping" event.
    echo "event: ping\n";
    $curDate = date(DATE_ISO8601);
    echo 'data: {"time": "'.$curDate.'"}';
    echo "\n\n";
    // Send a simple message at random intervals.
    --$counter;
    if (!$counter) {
        echo 'data: This is a message at time '.$curDate."\n\n";
        $counter = rand(1, 10);
    }
    ob_end_flush();
    flush();
    // Break the loop if the client aborted the connection (closed the page)
    if (connection_aborted()) {
        break;
    }
    sleep(1);
}
```

```sh
php -S 127.0.0.1 server.php
```


# Advanced 高级用法

```php

// construct usage
$client = new Roiwk\SSEClient\Client('http://127.0.0.1:8888', [
    'retryInterval' => 3,
    'onmessage' => function(string $data){},
    'streamContextOptions' => [
        'http' => [
            'method' => 'GET',
        ]
    ],
]);

// method usage
$client = new Roiwk\SSEClient\Client('http://127.0.0.1:8888');
$client->onmessage(function(string $data){
    echo $data.PHP_EOL;
});
$client->setRetryInterval(1);



```






