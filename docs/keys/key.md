---
id: key
title: Redis Keys
sidebar_label: Redis Keys
---

## Introduction

Redis keys are binary safe, this means that you can use any binary sequence as a key, from a string like "foo" to the
 content of a JPEG file. The empty string is also a valid key in **Redis**, but due to maintaining consistency in
  this package it's not supported. 
  
Read more about [redis keys](https://redis.io/topics/data-types-intro#redis-keys).
  
## Usage
You can create a key by instantiating an object from `Imdhemy\Redis\Support\Key` class:
```php
use Imdhemy\Redis\Support\Key;

$key = new Key('foo-key');
```

By default, the `Key` object uses `:` as a separator. You can edit the key separator by passing a second parameter
. Check the following examples:

```php
$userKey = new Key("user:1000");
$theSameUserKey = new Key("user:1000", ":");
$anotherUserKey = new Key("user-100", "-");
```

Try to stick with a schema. For instance `user:100` is a good idea. Dots or dashes are often used for multi-word
 fields, as in `comment:1234:reply.to` or `comment:1234:reply-to`.
 
Yoy can get the key segments using the `getParts()` method that returns an array of the key segments:
```php
$key = new Key('comment:123:reply');
$segments = $key->getParts(); // ['comment', 123, 'reply']
```
