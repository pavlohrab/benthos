---
title: bloblang
type: input
status: beta
categories: ["Utility"]
---

<!--
     THIS FILE IS AUTOGENERATED!

     To make changes please edit the contents of:
     lib/input/bloblang.go
-->

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

BETA: This component is mostly stable but breaking changes could still be made outside of major version releases if a fundamental problem with the component is found.

Generates messages at a given interval using a [Bloblang](/docs/guides/bloblang/about)
mapping executed without a context. This allows you to generate messages for
testing your pipeline configs.

```yaml
# Config fields, showing default values
input:
  bloblang:
    mapping: ""
    interval: 1s
    count: 0
```

## Fields

### `mapping`

A [bloblang](/docs/guides/bloblang/about) mapping to use for generating messages.


Type: `string`  
Default: `""`  

```yaml
# Examples

mapping: root = "hello world"

mapping: root = {"test":"message","id":uuid_v4()}
```

### `interval`

The time interval at which messages should be generated. If set to an empty string messages will be generated as fast as downstream services can process them. The first message emitted is always instant.


Type: `string`  
Default: `"1s"`  

### `count`

An optional number of messages to generate, if set above 0 the specified number of messages is generated and then the input will shut down.


Type: `number`  
Default: `0`  

## Examples

You can use Bloblang to generate payloads of differing structure at random:

```yaml
input:
  bloblang:
    mapping: |
      root = if random_int() % 2 == 0 {
        {
          "type": "foo",
          "foo": "is yummy"
        }
      } else {
        {
          "type": "bar",
          "bar": "is gross"
        }
      }
```

