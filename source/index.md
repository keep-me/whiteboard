---
title: API 参考文档

language_tabs:
  - bash
  - ruby
  - python
  - javascript

toc_footers:
  - <a href='#'>注册开发者密钥</a>
  - <a href='http://github.com/mpociot/whiteboard'>由 Whiteboard 提供的文档系统</a>

includes:
  - errors

search: true
---

# 简介

欢迎使用 Kittn API！您可以使用我们的 API 访问 Kittn API 接口，获取数据库中各种猫咪、幼猫和品种的信息。

我们提供了 Shell、Ruby、Python 和 JavaScript 等多种语言的代码示例！您可以在右侧深色区域查看代码示例，并通过右上角的标签切换示例的编程语言。

这个示例 API 文档页面是使用 [Whiteboard](http://github.com/mpociot/whiteboard) 创建的。您可以自由编辑它，并将其作为您自己 API 文档的基础。

# 身份认证

> 使用以下代码进行授权：

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
```

```bash
# 使用 Shell，您只需在每个请求中添加正确的请求头
curl "api_endpoint_here"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

const api = kittn.authorize('meowmeowmeow');
```

> 请确保将 `meowmeowmeow` 替换为您的 API 密钥。

Kittn 使用 API 密钥来控制 API 访问权限。您可以在我们的[开发者门户](http://example.com/developers)注册新的 Kittn API 密钥。

Kittn 要求在所有发送到服务器的 API 请求中，都需要在请求头中包含如下所示的 API 密钥：

`Authorization: meowmeowmeow`

<aside class="notice">
您必须将 <code>meowmeowmeow</code> 替换为您的个人 API 密钥。
</aside>

# 猫咪管理

## 获取所有猫咪

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```bash
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

const api = kittn.authorize('meowmeowmeow');
api.kittens.get();
```

> 以上命令返回的 JSON 结构如下：

```json
[
  {
    "id": 1,
    "name": "毛茸茸",
    "breed": "三色猫",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "麦克斯",
    "breed": "未知",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

此接口用于获取所有猫咪信息。

### HTTP 请求

`GET http://example.com/api/kittens`

### 查询参数

参数 | 默认值 | 描述
--------- | ------- | -----------
include_cats | false | 如果设置为 true，结果将同时包含成年猫咪。
available | true | 如果设置为 false，结果将包含已被领养的猫咪。

<aside class="success">
记住 — 一只快乐的猫咪是经过身份认证的猫咪！
</aside>

## 获取指定猫咪

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```bash
curl "http://example.com/api/kittens/2"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

const api = kittn.authorize('meowmeowmeow');
api.kittens.get(2);
```

> 以上命令返回的 JSON 结构如下：

```json
{
  "id": 2,
  "name": "麦克斯",
  "breed": "未知",
  "fluffiness": 5,
  "cuteness": 10
}
```

此接口用于获取指定猫咪的信息。

<aside class="warning">如果您不使用管理员 API 密钥，请注意有些仅对管理员隐藏的猫咪将返回 403 禁止访问。</aside>

### HTTP 请求

`GET http://example.com/kittens/<ID>`

### URL 参数

参数 | 描述
--------- | -----------
ID | 要获取的猫咪 ID
