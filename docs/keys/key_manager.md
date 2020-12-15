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
            <li><a href="#gettl">getTTL</a></li>
            <li><a href="#gettlms">getTTLMs</a></li>
            <li><a href="#keys">keys</a></li>
            <li><a href="#match">match</a></li>
            <li><a href="#pexpire">pExpire</a></li>
            <li><a href="#pexpireat">pExpireAt</a></li>
            <li><a href="#pttl">pTTl</a></li>
            <li><a href="#persist">persist</a></li>
            <li><a href="#randomkey">randomKey</a></li>
            </ul>
         </div>
    </div>
    <div class="blockElement threeByGridBlock">
          <div class="blockContent">
           <ul style="list-style-type: none">
            <li><a href="#rename">rename</a></li>
            <li><a href="#renameifavailable">renameIfAvailable</a></li>
            <li><a href="#renamenx">renameNx</a></li>
            <li><a href="#restore">restore</a></li>
            <li><a href="#setttl">setTTL</a></li>
            <li><a href="#setttlms">setTTLMs</a></li>
            <li><a href="#touch">touch</a></li>
            <li><a href="#ttl">ttl</a></li>
            <li><a href="#type">type</a></li>    
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
Is an alias for [ttl](#ttl).
```php
$ttl = $keyManager->getTTl($key);
```

### getTTLMs
Is an alias for [pExpire](#pexpire).

```php
$ttlMs = $keyManager->getTTlMs($key);
```

### keys
Returns all keys matching the specified pattern. Supported glob-style patterns:
- `h?llo` matches hello, hallo and hxllo
- `h*llo` matches hllo and heeeello
- `h[ae]llo` matches hello and hallo, but not hillo
- `h[^e]llo` matches hallo, hbllo, ... but not hello
- `h[a-b]llo` matches hallo and hbllo
- Use `\` to escape special characters if you want to match them verbatim.

> Warning: consider <code>keys()</code> as a command that should only be used in production environments with extreme care. It may ruin performance when it is executed against large databases. 

```php
$keys = $keyManager->keys('*name*');
```

### match
Is an alias for [keys](#keys).
```php
$keys = $keyManager->match('*name');
```

### pExpire
This method works exactly as [expire](#expire) but the time to live of the key is specified in milliseconds instead of seconds. Returns `true` if the timeout was set.
```php
$expires = $keyManager->pExpire($key, 1500);
```

### PExpireAt
This method has the same effect and semantic as [expireAt](#expireat), but the Unix time at which the key will expire is specified in milliseconds instead of milliseconds.
```php
$expire = $keyManager->pExpireAt($key, 1555555555005);
```

### pTTL
Get the time to live in milliseconds.
```php
$ttlMs = $keyManager->pTTL($key);
```

### persist
Remove the expiration from a key. Returns `false` if the ket does not exist.
```php
$perist = $keyManager->persist($key);
```

### randomKey
Returns a random key from the keyspace, or `null` if the keyspace is empty.
```php
$randomKey = $keyManager->randomKey();
```

### rename
Renames `$key` to `$newKey`.
```php
$keyManager->rename($key, $newKey);
```

### renameIfAvailable
Is an alias for [renameNx](#renamenx).
```php
$renamed = $keyManager->renameIfAvailable($key, $newKey);
```

### renameNx
Rename a `$key`, only if the `$newKey` is available. Returns `true` if renamed.
```php
$renamed = $keyManager->renameNx($key, $newKey);
```

### restore
Create a key using the provided serialized value, previously obtained using [dump](#dump). Returns `true` if the key was restored.

```php
$dump = $keyManager->dump($key);
$keyManager->delete($key);
$restored = $keyManager->restore($dump);
```

### setTTL
This is an alias for [expire](#expire).
```php
$expire = $keyManager->setTTl($key, $seconds);
```

### setTTLMs
This is an alias for [pExpire](#pexpire).
```php
$expires = $keyManager->setTTLMs($key, 1500);
```
### touch
Alters the last access time of a key.
```
$touched = $keyManager->touch($key);
```
### ttl
Get the time to live for a key.
- Returns how many seconds a given key will continue to be part of the dataset.
- returns `-2` if the key does not exist.
- returns `-1` if the key exists but has no associated expire.
```
$ttl = $keyManager->ttl($key);
```

### type
Determine the type stored at key.

| Standard Type | Returned Contract |
| --- | --- |
| string | `Imdhemy\Redis\Contracts\DataTypes\RedisString` |
| list | `Imdhemy\Redis\Contracts\DataTypes\RedisList` |
| set | `Imdhemy\Redis\Contracts\DataTypes\RedisSet` |
| zset | `Imdhemy\Redis\Contracts\DataTypes\RedisSortedSet` |
| hash | `Imdhemy\Redis\Contracts\DataTypes\RedisHashMap` |
| stream | `Imdhemy\Redis\Contracts\DataTypes\RedisStream` |
