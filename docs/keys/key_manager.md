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
                <li><a href="#">del</a></li>
                <li><a href="#">delete</a></li>
                <li><a href="#">delMany</a></li>
                <li><a href="#">deleteMany</a></li>
                <li><a href="#">dump</a></li>
                <li><a href="#">exists</a></li>
                <li><a href="#">expire</a></li>
                <li><a href="#">expireAtDatetime</a></li>
                <li><a href="#">expireAtTimestamp</a></li>
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

### delete
Is an alias for [del](#del).

### delMany
Removes multiple keys. Accepts an array of `Key` objects. Returns the number of deleted keys.

### deleteMany
Is an alias for [delMany](#delmany)

### dump
### exists
### expire
### expireAtDatetime
### expireAtTimestamp
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
