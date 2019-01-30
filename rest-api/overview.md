### 概述

**Catapult REST API**结合了HTTP和WebSockets在NEM区块链中执行读写操作。

### 请求

**Catapult REST**使用端口`3000`，并接受HTTP GET，PUT和POST请求。

假设Catapult REST在本地运行，HTTP GET请求可以从浏览器执行并具有以下形式：

```
http://localhost:3000/<path-to-API-request>
```


HTTP PUT和POST请求在request body中使用JSON结构。请求使用JSON结构返回数据（如果有任何返回）。

!> 除非您使用允许您执行此操作的插件，否则通常无法在浏览器中执行此类请求。

### Http 错误码

|Status code|说明|
|:---|:---|
|200|Ok。请求已成功|
|202|Accepted。该请求已被接受并处理，但处理尚未完成|
|400|Bad request。检查请求格式|
|404|Not found。资源不存在|
|409|Conflict。检查参数|
|500|内部错误|

### Http status

|Key|说明|
|:---|:---|
|code|定义好的错误标识符|
|message|以人类可读的格式解释错误|

**示例**

```
{
  "code": "InvalidArgument",
  "message": "accountId has an invalid format"
}
```

### uint64: lower和higher

Javascript只能表达32位值。为了使表达最多达到64位，API返回两部分编码的数字：`lower`和`higher`。

查看 [Check how to compact lower and higher into a simple number](https://github.com/nemtech/nem2-library-js/blob/f171afb516a282f698081aea407339cfcd21cd63/src/coders/uint64.js#L37).
