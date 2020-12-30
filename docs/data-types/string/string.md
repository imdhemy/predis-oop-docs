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
     <!-- Element End -->
          <!-- Element Start -->
             <div class="blockElement threeByGridBlock">
                 <div class="blockContent">
                     <ul style="list-style-type: none">
                          <li><a href="#bitfield">bitField</a></li>
                     </ul>
                 </div>
             </div>
          <!-- Element End -->
</div>

### append
Appends a value to current string value and sets the new length of the string value.

```php
$str->set('foo');
$length = $redisString->getLength(); // 3

$str->append('bar');
$length = $redisString->getLength(); // 6
```

### bitCount
Count the number of set bits (population counting) in a string. It is possible to specify the counting operation only in an interval passing the additional arguments `start` and `end`.

The arguments `start` and `end` can contain negative values in order to index bytes starting from the end of the string, where `-1` is the last byte, `-2` is the penultimate, and so forth.

```php
$redisString->set('foobar');

$bitCount = $redisString->bitCount(); // 26
$bitCount = $redisString->bitCount(0,0); // 4
$bitCount = $redisString->bitCount(1,1); // 6
```

### bitField
This method treats a Redis String as an array of bits. Using this method [you can set](#bitfieldset), for example a signed 5 bits integer at bit offeset 1234 to a specific value, retrieve a 31 bit unsigned integer from offset 4567. Similarly the command handles increments and decrements of the specified integers, providing guaranteed and well specified overflow and underflow behavior that the user can configure.

`bitField` is able to operate on multiple bit fields in the same command call. It takes a list of operations to perform, and returns an array of replies, where each array matches the corresponding operation in the list of arguments.

```php
// The following code increments an 5 bit signed integer at bit offset 100,
// and gets the value of the 4 bit unsigned integer at bit offset 0

$response = $redisString->bitField(
    RedisString::INCRBY, // increment by command
    'i5' // type: 5 bit signed integer
    100, // at bit offset 100,
    1, // increment by 1
    RedisString::GET, // Get command
    'u4', // 4 bit unsigned integer
    0, // at bit offset 0
);
```

`bitField` is variadic, you can [add multiple commands at one time](https://redis.io/commands/bitfield#supported-subcommands-and-integer-types), below is a list of available commands and arguments
- `[GET type offset]`
- `[SET type offset value]`
- `[INCRBY type offset increment]`
- `[OVERFLOW WRAP|SAT|FAIL]`

### bitFieldSet
Works the same as [bitField](#bitfield), but uses the `SET` subcommand:
```php
$type = '0u8';
$offset = '#0';
$value = 22;

$response = $redisString->bitFieldSet($type, $offset, $value);
```

### bitFieldGet
Works the same as [bitField](#bitfield), but uses the `GET` subcommand, and `WRAP` as an overflow control by default:
```php
$type = 'u8';
$offset = '#0';

$response = $redisString->bitFieldGet($type,$offset);

// You can optionally assign the overflow control as a third parameter
$response =  $redisString->bitFieldGet($type,$offset, RedisString::SAT);
```

### bitFieldIncrementBy
Works the same as [bitField](#bitfield), but uses the `INCRBY` subcommand, and `WRAP` as an overflow control by default:

```php
$type = 'u8';
$offset = '#0';
$increment = 5;

$response = $redisString->bitFieldIncrementBy($type, $offset, $increment);

// You can optionally assign the overflow control as a third parameter
$response = $redisString->bitFieldIncrementBy($type, $offset, $increment, RedisString::FAIL);
```
