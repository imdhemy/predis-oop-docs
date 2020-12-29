---
id: string
title: String
sidebar_label: String
---

## Introduction
Strings are the most basic kind of Redis value. Redis strings are binary safe, this means that a Redis string contains any kind of data, for instance a JPEG image, or a serialized PHP object. A string value can be at max 512 Megabytes in length.

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
     <!-- Element Start -->
        <div class="blockElement threeByGridBlock">
            <div class="blockContent">
                <ul style="list-style-type: none">
                     <li><a href="#bitcount">bitCount</a></li>
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

### bitCount
Count the number of set bits (population counting) in a string. It is possible to specify the counting operation only in an interval passing the additional arguments `start` and `end`.

The arguments `start` and `end` can contain negative values in order to index bytes starting from the end of the string, where `-1` is the last byte, `-2` is the penultimate, and so forth.

```php
$str->set('foobar');

$bitCount = $str->bitCount(); // 26
$bitCount = $str->bitCount(0,0); // 4
$bitCount = $str->bitCount(1,1); // 6
```