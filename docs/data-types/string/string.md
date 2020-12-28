---
id: string
title: String
sidebar_label: String
---

## Introduction
Strings are the most basic kind of Redis value. Redis strings are binary safe, this means that a Reid string contains any kind of data, for instance a JPEG image, or a serialized PHP object. A string value can be at max 512 Megabytes in length.

**You can do a number of interesting things using strings in Redis, for instance you can:**
- Use Strings as atomic counters using methods in the `increment` family: [increment](#increment), [decrement](#decrement), [incrementBy](#incrementby).
- Append to strings with the [append](#append) method.
- Use Strings as a random access vectors with [getRange](#getrange) and [setRange](#setrange).
- Encode a lot of data in little space, or create a Redis backed Bloom filter using [getBit](#getbit) and [setBit](#setbit).

This document contains much more methods, check the sidebar for all the available methods.

## Instantiation
To create a Redis String object:
```php
use Predis\Client;
use Imdhemy\Redis\Support\Key;
use Imdhemy\Redis\DataTypes\RedisString;

$client = new Client();
$key = new Key('foo-key');

$redisString = new RedisString($client, $key);
```

## Available Methods
Below is a list of all available methods and their function:

<div class="gridBlock">
   <!-- Element Start -->
    <div class="blockElement threeByGridBlock">
        <div class="blockContent">
            <ul style="list-style-type: none">
                 <li><a href="#append">append</a></li>
            </ul>
        </div>
    </div>
    <!-- Element End -->
</div>

### append
Appends a value to current string value and sets the new length of the string value.

```php
$str->set('foo');
$length = $str->getLength(); // 3

$str->append('bar');
$length = $str->getLength(); // 6
```
