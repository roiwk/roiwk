+++
author = "roiwk"
title = "友盟openAPI的php实现"
description = "友盟openAPI的php实现"
date = "2020-12-09"
keywords = [
    "umeng openapi",
    "php umeng openapi",
    "composer"
]
tags = [
    "php",
    "umeng",
    "composer",
]
categories = [
    "php",
]
draft = false
+++


<p>
 <a href="https://gitee.com/roiwk/UmengOpenAPI">
    <img src="https://img.shields.io/badge/roiwk/UmengOpenAPI-C71D23?logo=gitee" alt="gitee" title="roiwk/UmengOpenAPI"/>
  </a>

 <a href="https://github.com/roiwk/UmengOpenAPI">
    <img src="https://img.shields.io/badge/roiwk/UmengOpenAPI-181717?logo=github" alt="github" title="github/UmengOpenAPI"/>
  </a>
</p>

![Packagist Downloads](https://img.shields.io/packagist/dt/roiwk/umeng-open-api)

# 简介

一个简单,好用的友盟open-api的包...
封装了友盟官方open-api的sdk, 官方sdk版本1.1.4

> [umeng官方文档](https://developer.umeng.com/open-api/state)

## 安装

```shell
composer require roiwk/umeng-open-api
```

## 快速使用

例子: 获取应用的累计用户数
[此示例的umeng文档](https://developer.umeng.com/open-api/docs/com.umeng.umini/umeng.umini.getTotalUser/1)

```php

require_once 'path/to/autoload.php';

use Roiwk\UmengOpenAPI\Factory;

// 工厂类中，有具体的小程序，app等应用类型，详见源码即可
$app = Factory::umini([
    'api_key'       => 'your key',
    'api_secret'    => 'your secret',
    'app_key'       => 'your APPKEY',
    // 指定 API 调用返回结果的类型：json(default)/array/object/raw(resultObject)
    'response_type' => 'json',
]);

// 参数1:api名 (com.umeng.umini:umeng.umini.getTotalUser-1, 传"getTotalUser" 即可)
// 参数2: 请求参数数组
$app->get('getTotalUser', [
    'fromDate'  => '2020-11-01',
    'toDate'    => '2020-11-01',
    'pageIndex' => 1,
    'pageSize'  => 10,
]);
```

## 项目缘由

友盟官方的sdk, 在已有的composer项目中,用起来很不方便, 所以封装一个用.

## 贡献

欢迎提交PR

## 开源许可协议 - MIT

 [MIT LICENSE - Gitee Storage](https://gitee.com/roiwk/UmengOpenAPI/blob/master/LICENSE)

 [MIT LICENSE - Github Storate](https://github.com/roiwk/UmengOpenAPI/blob/master/LICENSE)
