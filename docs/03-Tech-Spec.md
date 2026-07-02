# 智慧农业生态园官网
Technical Specification（V1.0）

---

# 1. 技术目标

本项目采用现代 Web 开发模式，构建一个可维护、可扩展、易部署的企业级网站。

MVP 阶段重点关注：

- 清晰的代码结构
- 前后端分离
- RESTful API
- 模块化开发
- 良好的可维护性
- 为后续功能扩展预留空间

本项目不追求复杂架构，而追求合理、稳定、易理解。

---

# 2. 架构原则

整个系统遵循以下原则：

## Separation of Concerns

前端负责界面展示。

后端负责业务逻辑。

数据库负责数据持久化。

各层职责明确，不允许跨层访问。

---

## Single Responsibility

每个模块只负责一件事情。

一个组件只完成一种职责。

一个接口只解决一个业务问题。

---

## Component First

所有页面优先采用组件化设计。

禁止复制粘贴大量重复代码。

公共组件必须抽离。

---

## API First

前后端通过 HTTP API 通信。

页面不得直接访问数据库。

---

## Scalability

所有设计均应考虑未来扩展：

- 商城
- IoT
- VR
- 直播
- 小程序

---

# 3. 推荐技术方向

开发语言和框架不限。

建议选择成熟、长期维护、社区活跃的技术方案。

系统应满足：

- 前后端分离
- RESTful API
- ORM
- 文件上传
- 身份认证
- 响应式前端

避免使用已经停止维护或生态薄弱的框架。

---

# 4. 项目目录规范

## Frontend

frontend/

src/

components/

layouts/

pages/

router/

stores/

services/

assets/

styles/

utils/

types/

---

## Backend

backend/

controllers/

services/

repositories/

entities/

dtos/

middlewares/

configs/

utils/

uploads/

---

每个目录职责明确。

禁止随意堆放文件。

---

# 5. 命名规范

组件：

PascalCase

例如：

NewsCard

TraceTimeline

HeroBanner

---

变量：

camelCase

例如：

newsList

traceCode

currentUser

---

常量：

UPPER_SNAKE_CASE

例如：

MAX_UPLOAD_SIZE

DEFAULT_PAGE_SIZE

---

数据库：

snake_case

例如：

trace_record

page_content

---

接口路径：

小写

使用短横线。

例如：

/api/news

/api/products

/api/trace

---

# 6. 页面规范

一个页面负责一个业务。

页面只负责：

- 数据请求
- 页面布局

复杂逻辑应放入：

Service

Store

Hook

或业务层。

---

# 7. 组件规范

组件分为：

## Base Components

按钮

输入框

卡片

弹窗

标签

---

## Business Components

新闻卡片

产品卡片

时间轴

轮播图

导航栏

Footer

---

Base Component 不允许依赖业务。

Business Component 可组合 Base Component。

---

# 8. API 规范

统一使用 RESTful 风格。

例如：

GET

/api/news

GET

/api/news/{id}

POST

/api/news

PUT

/api/news/{id}

DELETE

/api/news/{id}

返回格式统一：

{
    "code": 200,
    "message": "success",
    "data": {}
}

错误格式：

{
    "code": 400,
    "message": "error",
    "data": null
}

---

# 9. 错误处理

所有异常必须统一处理。

不得直接向用户暴露异常堆栈。

接口应返回统一错误结构。

前端统一处理错误提示。

---

# 10. 文件上传

支持：

图片

PDF

上传文件统一管理。

保存文件路径。

数据库仅保存引用地址。

禁止保存二进制文件。

---

# 11. 日志规范

系统记录：

登录

新增

修改

删除

错误

日志统一输出。

方便后续排查问题。

---

# 12. 安全规范

管理员密码必须加密。

禁止明文保存。

后台接口必须认证。

重要操作建议记录日志。

防止 SQL 注入。

防止 XSS。

防止 CSRF。

---

# 13. Git 规范

分支：

main

develop

feature/*

Commit：

feat:

fix:

docs:

style:

refactor:

test:

chore:

每次 Commit 保持单一主题。

---

# 14. 代码质量

遵循：

SOLID

DRY

KISS

Clean Code

避免：

超长函数。

超大组件。

重复代码。

魔法数字。

硬编码。

---

# 15. 文档要求

所有模块应包含必要注释。

接口应同步维护 API 文档。

README 应包含：

项目介绍

启动方式

目录结构

部署说明

Roadmap

开发者无需阅读源码即可理解项目结构。