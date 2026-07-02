# 智慧农业生态园官网
# API Specification（V1.0）

---

# 1. 文档说明

本文档定义智慧农业生态园官网（MVP）所有 RESTful API。

所有接口均遵循统一规范。

API Version：

v1

Base URL：

/api/v1

---

# 2. 通用规范

## 请求格式

Content-Type

application/json

文件上传：

multipart/form-data

---

## 返回格式

所有接口统一返回：

```json
{
    "code": 200,
    "message": "success",
    "data": {}
}
```

---

请求失败：

```json
{
    "code": 400,
    "message": "error",
    "data": null
}
```

---

## HTTP 状态码

| 状态码 | 说明 |
|---------|------|
|200|成功|
|201|创建成功|
|204|删除成功|
|400|请求错误|
|401|未登录|
|403|没有权限|
|404|资源不存在|
|500|服务器错误|

---

## 分页规范

统一采用：

page

pageSize

返回：

```json
{
    "page":1,
    "pageSize":10,
    "total":100,
    "items":[]
}
```

---

# 3. 身份认证

MVP：

管理员登录。

认证方式：

Bearer Token

Authorization：

Bearer {token}

登录成功后：

前端保存 Token。

后续请求统一携带 Authorization Header。

---

# 4. 登录接口

## 管理员登录

POST

/api/v1/auth/login

Request

```json
{
    "username":"admin",
    "password":"123456"
}
```

Response

```json
{
    "code":200,
    "message":"success",
    "data":{
        "token":"xxxxx",
        "nickname":"Administrator"
    }
}
```

---

# 5. 新闻模块

## 获取新闻列表

GET

/api/v1/news

Query

| 参数 | 类型 |
|------|------|
|page|number|
|pageSize|number|

Response

```json
{
    "page":1,
    "pageSize":10,
    "total":20,
    "items":[]
}
```

---

## 获取新闻详情

GET

/api/v1/news/{id}

---

## 新增新闻

POST

/api/v1/news

---

## 修改新闻

PUT

/api/v1/news/{id}

---

## 删除新闻

DELETE

/api/v1/news/{id}

---

# 6. 页面内容

## 获取页面内容

GET

/api/v1/pages/{pageKey}

例如：

about

home

park

---

## 更新页面内容

PUT

/api/v1/pages/{pageKey}

---

# 7. 产品模块

## 产品列表

GET

/api/v1/products

---

## 产品详情

GET

/api/v1/products/{id}

---

## 新增产品

POST

/api/v1/products

---

## 修改产品

PUT

/api/v1/products/{id}

---

## 删除产品

DELETE

/api/v1/products/{id}

---

# 8. 溯源查询

## 根据溯源码查询

GET

/api/v1/trace/{traceCode}

Response

```json
{
    "code":200,
    "message":"success",
    "data":{
        "product":{},
        "timeline":[]
    }
}
```

---

# 9. 溯源记录

## 获取时间轴

GET

/api/v1/products/{id}/trace-records

---

## 新增节点

POST

/api/v1/products/{id}/trace-records

---

## 修改节点

PUT

/api/v1/trace-records/{id}

---

## 删除节点

DELETE

/api/v1/trace-records/{id}

---

# 10. 文件上传

上传图片

POST

/api/v1/upload/image

Content-Type

multipart/form-data

返回：

```json
{
    "code":200,
    "message":"success",
    "data":{
        "url":"https://..."
    }
}
```

---

上传 PDF

POST

/api/v1/upload/file

---

# 11. 错误码

| Code | 含义 |
|------|------|
|200|成功|
|400|请求参数错误|
|401|未登录|
|403|权限不足|
|404|资源不存在|
|409|数据冲突|
|422|数据校验失败|
|500|服务器异常|

---

# 12. API 设计原则

遵循：

- RESTful
- Resource Oriented
- Stateless
- JSON
- HTTP Standard

URL 使用：

名词

例如：

/products

/news

/pages

避免：

/getNews

/queryTrace

/deleteProduct

使用 HTTP Method 表达行为。

---

# 13. 接口命名规范

资源：

复数名词。

例如：

products

news

pages

上传：

upload

认证：

auth

所有 URL：

小写。

短横线。

例如：

trace-records

禁止：

CamelCase

禁止：

下划线。

---

# 14. 安全要求

后台接口：

必须认证。

公共接口：

无需登录。

上传：

限制文件大小。

限制文件类型。

禁止：

任意文件上传。

---

# 15. API 演进策略

API Version：

v1

未来升级：

v2

不得直接修改已有接口。

新增字段：

保持向后兼容。

删除字段：

必须经过版本升级。

所有接口应保证稳定性。