# 智慧农业生态园官网
# System Architecture（V1.0）

---

# 1. 文档说明

本文档描述智慧农业生态园官网（MVP）的整体系统架构、模块划分、数据流向及设计原则。

目标：

- 明确系统整体结构
- 指导后续开发
- 保持系统可维护、可扩展
- 为未来版本（商城、IoT、直播等）预留扩展能力

---

# 2. 架构目标

系统遵循以下目标：

- 前后端分离
- RESTful API
- 模块化设计
- 高内聚、低耦合
- 易维护
- 易扩展
- 易部署

MVP 阶段采用简单稳定的架构，不引入不必要的复杂设计。

---

# 3. 系统总体架构

```text
                    用户浏览器
                          │
                    HTTP / HTTPS
                          │
          ┌──────────────────────────┐
          │      Frontend Web         │
          │      企业官网（SPA）        │
          └──────────────────────────┘
                          │
                     RESTful API
                          │
          ┌──────────────────────────┐
          │      Backend API          │
          │    业务逻辑 / 身份认证      │
          └──────────────────────────┘
                          │
          ┌──────────────────────────┐
          │         Database          │
          │         MySQL             │
          └──────────────────────────┘
```

---

# 4. 系统模块

## 前台（Frontend）

负责：

- 页面展示
- 用户交互
- 数据请求
- 响应式布局

包含模块：

- 首页
- 园区介绍
- 产品溯源
- 新闻资讯
- 关于我们

---

## 后台（Admin）

负责：

- 管理员登录
- 页面内容管理
- 新闻管理
- 产品溯源管理

---

## API 服务（Backend）

负责：

- 身份认证
- 业务逻辑
- 数据校验
- 文件上传
- 数据持久化

所有客户端均通过 API 与后台通信。

---

## 数据库（Database）

负责：

- 管理员数据
- 新闻数据
- 页面内容
- 产品信息
- 溯源记录

数据库仅负责数据存储，不承担业务逻辑。

---

# 5. 模块关系

```text
Browser
    │
    ▼
Frontend
    │
    ▼
REST API
    │
    ▼
Controller
    │
    ▼
Service
    │
    ▼
Repository
    │
    ▼
Database
```

依赖关系必须保持单向，不允许跨层调用。

---

# 6. 数据流

## 新闻查询

```text
Browser
    │
GET /api/news
    │
    ▼
Controller
    │
    ▼
Service
    │
    ▼
Repository
    │
    ▼
Database
    │
    ▼
Repository
    │
    ▼
Service
    │
    ▼
Controller
    │
JSON
    │
    ▼
Browser
```

---

## 产品溯源查询

```text
Browser
    │
输入溯源码
    │
    ▼
GET /api/trace/{traceCode}
    │
    ▼
Controller
    │
    ▼
Service
    │
    ▼
Repository
    │
    ▼
Database
    │
    ▼
返回产品信息
    │
    ▼
时间轴数据
    │
    ▼
Browser
```

---

# 7. 模块职责

## Frontend

负责：

- 页面展示
- 用户交互
- API 请求
- 数据渲染

不负责：

- 数据库存取
- 权限判断
- 业务规则

---

## Backend

负责：

- 所有业务逻辑
- 参数校验
- 权限控制
- 文件上传
- 数据处理

不负责：

- 页面渲染
- UI 展示

---

## Database

负责：

- 数据持久化

不负责：

- 业务逻辑
- 权限控制

---

# 8. 页面结构

```text
Layout
│
├── Header
├── Main
│
│   ├── Home
│   ├── Park
│   ├── Trace
│   ├── News
│   └── About
│
└── Footer
```

所有页面共享统一 Layout。

---

# 9. 前端组件结构

```text
components
│
├── common
│   ├── Button
│   ├── Card
│   ├── Input
│   ├── Dialog
│   └── Pagination
│
├── layout
│   ├── Header
│   ├── Footer
│   └── Container
│
├── home
│   ├── HeroBanner
│   ├── ParkOverview
│   ├── BusinessSection
│   ├── TraceEntry
│   └── NewsSection
│
├── news
│   ├── NewsCard
│   ├── NewsList
│   └── NewsDetail
│
└── trace
    ├── TraceSearch
    ├── TraceTimeline
    └── TraceReport
```

组件必须职责单一，可复用。

---

# 10. 后端模块结构

```text
backend
│
├── auth
├── news
├── page
├── product
├── trace
├── upload
└── common
```

每个业务模块包含：

- Controller
- Service
- Repository
- Entity
- DTO

业务之间禁止直接耦合。

---

# 11. 系统边界

MVP 阶段包含：

- 企业官网
- 后台管理
- 产品溯源

暂不包含：

- 商城
- 支付
- 预约
- IoT
- 直播
- VR
- 数据大屏

上述模块将在后续版本通过 API 扩展接入。

---

# 12. 扩展规划

未来系统支持扩展：

```text
                Browser
                    │
         ┌──────────┴──────────┐
         │                     │
      Website               Mobile App
         │                     │
         └──────────┬──────────┘
                    │
               RESTful API
                    │
      ┌─────────────┼─────────────┐
      │             │             │
   Admin        IoT Service    Live Service
      │             │             │
      └─────────────┴─────────────┘
                    │
                 Database
```

保持 API 作为唯一业务入口。

---

# 13. 架构原则

开发过程中必须遵循：

- 单一职责（Single Responsibility）
- 模块化（Modular Design）
- 前后端分离（Separation of Concerns）
- API First
- 可扩展（Scalable）
- 可维护（Maintainable）
- 高内聚、低耦合（High Cohesion, Low Coupling）

禁止：

- 页面直接访问数据库
- Controller 编写业务逻辑
- Repository 处理业务规则
- 跨层调用
- 重复实现相同业务

---

# 14. 文档维护

当系统架构发生重大调整时，应同步更新本文件。

所有新增模块必须符合本架构设计，不得破坏整体一致性。