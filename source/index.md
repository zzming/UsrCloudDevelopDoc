---
title: UsrCloud.dll 用户手册

language_tabs:

  - pascal
  - csharp
  - cpp
  - vb

toc_footers:
  - 版本  :1.0
  - 日期  :2017-5-4
  - <a href='http://www.usr.cn'>有人物联网</a>

search: true
---

# 1. 快速上手
todo 展示最基本的流程

# 2. 接口说明

## 2.1. 初始化和释放

### 2.1.1. <aside class="notice">USR_GetVer 获取dll版本
</aside>

> USR_GetVer 获取dll版本 用法示例:

```pascal
todo Delphi示例
```
```csharp
todo C#示例
```
```cpp
todo C++示例
```
```vb
todo vb示例
```

<br>

**函数原型:<br><br>`long USR_GetVer();`**

返回值| 描述
---- | ----
long| DLL版本号

### 2.1.2. <aside class="notice">USR_Init 初始化接口
</aside>

> USR_Init 初始化接口 用法示例:

```pascal
todo Delphi示例
```
```csharp
todo C#示例
```
```cpp
todo C++示例
```
```vb
todo VB示例
```

<br>

**函数原型:<br><br>`boolean USR_Init(LPCWSTR Host, unsigned short Port, long Ver);`**

参数| 描述
---- | ----
Host|[in] 透传云服务器地址 cloud.usr.cn
Port|[in] 端口 1883
Ver |[in] 指定你想使用的版本号,必须 <= 函数USR_GetVer查询到的最高版本号,目前只能填 1。

返回值| 描述
---- | ----
boolean| 成功返回 true ,失败返回 false

### 2.1.3. <aside class="notice">USR_Release 释放接口
</aside>

> USR_Release 释放接口 用法示例:

```pascal
todo Delphi示例
```
```csharp
todo C#示例
```
```cpp
todo C++示例
```
```vb
todo VB示例
```

<br>

**函数原型:<br><br>`boolean USR_Release();`**

返回值| 描述
---- | ----
boolean| 成功返回 true ,失败返回 false


## 2.2. 连接和断开

### 2.2.1. <aside class="notice">USR_OnConnAck 设置 连接响应 回调函数
</aside>

> USR_OnConnAck 设置 连接响应 回调函数 用法示例:

```pascal
todo Delphi示例
```
```csharp
todo C#示例
```
```cpp
todo C++示例
```
```vb
todo VB示例
```

<br>

**函数原型:<br><br>`boolean USR_OnConnAck(TUSR_ConnAckEvent OnConnAct);`**

参数|描述
----|----
OnConnAct |[in] 连接响应 回调函数   [TUSR_ConnAckEvent 定义](#Define_TUSR_ConnAckEvent)

返回值| 描述
---- | ----
boolean| 成功返回 true ,失败返回 false

<span id = "Define_TUSR_ConnAckEvent"></span>
#### 2.2.1.1. **TUSR_ConnAckEvent 定义:**

<br>

**`typedef void(__stdcall *TUSR_ConnAckEvent)(
                long ReturnCode,
                LPCWSTR Description
                );`**

参数|描述
----|----
ReturnCode |[in] 返回码
Description|[in] 返回码代表的含义

返回值|描述
----|----
boolean|成功返回 true ,失败返回 false

可能的返回码如下:

返回码|返回码代表的含义
----|----
0x00 |连接已接受
0x01 |连接已拒绝，不支持的协议版本
0x02 |连接已拒绝，不合格的客户端标识符
0x03 |连接已拒绝，服务端不可用
0x04 |连接已拒绝，无效的用户名或密码
0x05 |连接已拒绝，未授权

### 2.2.2. <aside class="notice">USR_Connect 连接
</aside>

> USR_Connect 连接 用法示例:

```pascal
todo Delphi示例
```
```csharp
todo C#示例
```
```cpp
todo C++示例
```
```vb
todo VB示例
```

<br>

**函数原型:<br><br>`boolean USR_Connect(LPCWSTR Username, LPCWSTR Password);`**

参数| 描述
---- | ----
Username|[in] 用户名
Password|[in] 密码

返回值| 描述
---- | ----
boolean| 返回true说明两个问题:<br>(1).成功和服务器建立了TCP连接<br>(2).成功将用户名、密码等验证信息发给了服务器。<br><br>最终有没有被服务器所接受,要通过USR_OnConnAck设置的回调函数来判断。

### 2.2.3. <aside class="notice">USR_DisConnect 断开连接
</aside>

> USR_DisConnect 断开连接 用法示例:

```pascal
todo Delphi示例
```
```csharp
todo C#示例
```
```cpp
todo C++示例
```
```vb
todo VB示例
```

<br>

**函数原型:<br><br>`boolean USR_DisConnect();`**

返回值| 描述
---- | ----
boolean| 成功返回 true ,失败返回 false

## 2.3. 订阅消息


### 2.3.1. <aside class="notice">USR_OnSubAck 设置 订阅响应 回调函数
</aside>

> USR_OnSubAck 设置 订阅响应 回调函数 用法示例:

```pascal
todo Delphi示例
```
```csharp
todo C#示例
```
```cpp
todo C++示例
```
```vb
todo VB示例
```

<br>

**函数原型:<br><br>`boolean USR_OnSubAck(TUSR_SubAckEvent OnSubAck);`**

参数|描述
----|----
OnSubAck |[in] 订阅响应 回调函数   [TUSR_SubAckEvent 定义](#Define_TUSR_SubAckEvent)

返回值| 描述
---- | ----
boolean| 成功返回 true ,失败返回 false

<span id = "Define_TUSR_SubAckEvent"></span>
#### 2.3.1.1. **TUSR_SubAckEvent 定义:**

<br>

**`typedef void(__stdcall *TUSR_SubAckEvent)(
                long MessageID,
                LPCWSTR DevId,
                LPCWSTR ReturnCode
                );`**

参数|描述
----|----
MessageID |[out] 消息ID,一般用不到
DevId |[out] 设备ID,多个用逗号隔开
ReturnCode |[out] 返回码,表示订阅结果,多个用逗号隔开,和DevId依次对应。

返回值|描述
----|----
boolean|成功返回 true ,失败返回 false




# 3. 更新历史

版本 | 更新内容 | 负责人
--------- | ----------- | -----------
1.0 | 初版 | 张振鸣

<aside class="notice">提示</aside>
<aside class="success">成功</aside>
<aside class="warning">警告</aside>