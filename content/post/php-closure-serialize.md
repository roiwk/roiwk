+++
author = "roiwk"
title = "php的闭包序列化"
description = "php闭包序列化，一些实现与对现有程序的思考。"
date = "2023-05-27"
keywords = [
    "php",
    "闭包",
    "php闭包",
    "序列化",
    "闭包序列化",
    "php闭包序列化",
    "closure",
    "serialized",
    "php closure serialized",
]
tags = [
    "php",
    "closure",
    "serialized",
]
categories = [
    "php",
]
draft = false
+++

# PHP 闭包序列化：实现和对现有程序的思考

在 PHP 中，闭包是一种非常强大的特性，可以让我们编写更简洁、更灵活的代码。然而，当我们需要将闭包序列化并保存到文件或数据库中时，可能会遇到一些问题。本文将介绍如何实现 PHP 闭包序列化，并探讨这一过程对现有程序的影响。

## 什么是闭包？

在 PHP 中，闭包是一种可以访问其定义范围内变量的函数。换句话说，它们可以捕获其创建时所处的上下文，并在稍后执行时访问该上下文。闭包通常用于创建回调函数、生成器和事件处理程序等。

以下是一个简单的闭包示例(好像又没那么简单)：

```php
$multiplier = function ($x) {
    return function ($y) use ($x) {
        return $x * $y;
    };
};

$double = $multiplier(2);
echo $double(5); // 输出 10
```

在上面的例子中，`$multiplier` 是一个接收一个参数 `$x` 的函数，它返回另一个接收一个参数 `$y` 的函数。返回的函数使用了 `$x`，这个值是从外部作用域中“捕获”的。

## 为什么需要序列化闭包？

在某些情况下，我们可能需要将闭包保存到文件或数据库中，以便稍后使用。例如，现有代码，需要异步处理时，又不想改动太大，我们就需要将现有执行逻辑打包，做成闭包后序列化并保存到数据库中，以便稍后异步执行。


## 实现闭包序列化

PHP 提供了 `serialize()` 和 `unserialize()` 函数，可以将大部分 PHP 数据类型序列化为字符串，并在稍后还原它们。然而，`serialize()` 和 `unserialize()` 函数不能正确地序列化闭包。

要序列化闭包，我们需要首先安装 `opis/closure` 包, 

```sh
composer require opis/closure
```

然后使用闭包序列化, (注意这里使用了包中的序列化函数)：

```php
use function Opis\Closure\{serialize, unserialize};

$factorial = function ($n) use (&$factorial) {
  return $n <= 1 ? 1 : $factorial($n - 1) * $n;
};

$serialized = serialize($wrapper);
```

要还原闭包，我们需要使用以下代码：

```php
use function Opis\Closure\{serialize, unserialize};

$wrapper = unserialize($serialized);

echo $wrapper(5);  // 输出：120

```


## 对现有程序的影响

1. 将闭包序列化后，它们的执行环境被固定在序列化时的状态。
   换句话说，如果您序列化了一个闭包，并将其保存到文件或数据库中，然后稍后还原它并尝试执行它，它将访问当时的变量值，而不是当前的变量值。 
2. 如果一个闭包使用了资源类型（如文件句柄），那么它就不能被序列化。 
如果您需要序列化这种类型的闭包，请考虑将其改为使用其他类型的变量，例如文件路径。 
3. 避免在序列化闭包时，闭包中传入了超大容量的参数(如数据库查询结果集)，这样会导致序列化后的字符串长度非常长。 
如果必须这样，可以考虑传查询条件，让其再闭包中去执行相关查询操作。

## 结论

在 PHP 中，序列化闭包是一项非常具有挑战性的任务。然而，通过使用 `opis/closure` ，我们可以非常简单地实现这个目标。然后大战拳脚吧。