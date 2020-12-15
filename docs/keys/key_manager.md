---
id: key_manager
title: Key Manager
sidebar_label: Key Manager
---

## Introduction

The key manager class `Imdhemy\Redis\Support\KeyManager` contains a wide variety of method that may apply to keys. We
'll cover each of these methods in detail so that you are familiar with all Predis-OOP's key features:

## Instantiation
The `KeyManager` object requires a `Predis\ClientInterface` in its constructor that is supported under the hood
 through `predis/predis` php package.
 
```php
use Predis\Client;
use Imdhemy\Redis\Support\KeyManager;

$client = new Client();
$keyManager = new KeyManager($client);
```

## Available Methods
Below is a list of all available methods and their function:

<div class="gridBlock">
    <div class="blockElement threeByGridBlock">
        <div class="blockContent">
            <ul style="list-style-type: none">
                <li><a href="#del">del</a></li>
                <li><a href="#delete">delete</a></li>
                <li><a href="#delmany">delMany</a></li>
                <li><a href="#deleteMany">deleteMany</a></li>
                <li><a href="#dump">dump</a></li>
                <li><a href="#exists">exists</a></li>
                <li><a href="#expire">expire</a></li>
                <li><a href="#expireat">expireAt</a></li>
                <li><a href="#expireatdatetime">expireAtDatetime</a></li>
                <li><a href="#expireattimestamp">expireAtTimestamp</a></li>
            </ul>
        </div>
    </div>
    <div class="blockElement threeByGridBlock">
         <div class="blockContent">
            <ul style="list-style-type: none">
            <li><a href="#">getTTL</a></li>
            <li><a href="#">getTTLMs</a></li>
            <li><a href="#">keys</a></li>
            <li><a href="#">match</a></li>
            <li><a href="#">pExpire</a></li>
            <li><a href="#">pExpireAt</a></li>
            <li><a href="#">pTTl</a></li>
            <li><a href="#">persist</a></li>
            <li><a href="#">randomKey</a></li>
            </ul>
         </div>
    </div>
    <div class="blockElement threeByGridBlock">
          <div class="blockContent">
           <ul style="list-style-type: none">
            <li><a href="#">rename</a></li>
            <li><a href="#">renameIfAvailable</a></li>
            <li><a href="#">renameNx</a></li>
            <li><a href="#">restore</a></li>
            <li><a href="#">setTTL</a></li>
            <li><a href="#">setTTLMs</a></li>
            <li><a href="#">touch</a></li>
            <li><a href="#">ttl</a></li>
            <li><a href="#">type</a></li>    
           </ul>
           </div>
    </div>
</div>

### del
Removes the specified key. Returns `true` if deleted or `false` if it does not exist.
```php
$isDeleted = $keyManager->del($key);
```

### delete
Is an alias for [del](#del).
```php
$isDeleted = $keyManager->delete($key);
```

### delMany
Removes multiple keys. Accepts an array of `Key` objects. Returns the number of deleted keys.
```php
$deletedKeyesCount = $keyManager->delMany([$key1, $key2, $key3]);
```

### deleteMany
Is an alias for [delMany](#delmany)
```php
$deletedKeyesCount = $keyManager->deleteMany([$key1, $key2, $key3]);
```

### dump
Returns a serialized version of the value stored at the specified key.
- It contains a 64-bit checksum.
- The [restore](#restore) method makes sure to check the checksum before synthesizing a key using the serialized value.
If the key does not exist a `null` value returned.
```php
$dump = $keyManager->dump($key);
```

### exists
Determine if a key exists.
```php
$exists = $keyManager->exists($key);
```

### expire
Set a key's time to live in seconds. Returns `false` if the key does not exist.
```php
$expire = $keyManager->expire($key, $seconds);
```

### expireAt
Has the same effect of [expire](#expire), but instead of specifying the number of seconds representing the TTL (time to live), it takes an absolute Unix timestamp (seconds since January 1, 1970). A timestamp in the past will delete the key immediately. It returns `true` if the timeout was set.
```php
$expire = $keyManager->expireAt($unixTimestamp);
```

### expireAtDatetime
Has the same effect of [expireAt](#expireat), but instead of specifying a Unix timestamp, it takes a `DateTime` object.
```php
$datetime = (new DateTime)->modify('+1 day');
$expire = $keyManager->expireAtDatetime($datetime);
```

### expireAtTimestamp
Is an alias for [expireAt](#expireat).
```php
$expire = $keyManager->expireAtTimestamp($unixTimestamp);
```

### getTTL
### getTTLMs
### keys
### match
### pExpire
### PExpireAt
### pTTL
### persist
### randomKey
### rename
### renameIfAvailable
### renameNx
### restore
### setTTL
### setTTLMs
### touch
### ttl
### type
