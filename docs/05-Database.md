# 智慧农业生态园官网
# Database Design（V1.0）

---

# 1. 文档说明

本文档定义智慧农业生态园官网（MVP）数据库设计。

目标：

- 建立统一的数据模型
- 保持数据库结构规范
- 支持后续业务扩展
- 为 API 开发提供数据基础

数据库设计遵循：

- 第三范式（3NF）
- 单一职责
- 可扩展
- 可维护

---

# 2. 数据库概览

MVP 阶段包含以下业务实体：

| 实体 | 说明 |
|------|------|
| Admin | 管理员 |
| News | 新闻资讯 |
| PageContent | 页面内容 |
| Product | 产品 |
| TraceRecord | 产品溯源记录 |

---

# 3. ER 关系

```text
Admin
    │
    ├──────────────┐
    │              │
    ▼              ▼
 News        PageContent

Product
    │
    │ 1
    │
    │
    ▼ N

TraceRecord
```

说明：

- 一个 Product 可以拥有多个 TraceRecord。
- 一个 TraceRecord 只属于一个 Product。
- Admin 负责维护 News、PageContent、Product。

---

# 4. 数据表设计

## 4.1 Admin

管理员账号。

| 字段 | 类型 | 约束 | 说明 |
|------|------|------|------|
| id | BIGINT | PK | 主键 |
| username | VARCHAR(50) | UNIQUE | 登录账号 |
| password | VARCHAR(255) | NOT NULL | 加密密码 |
| nickname | VARCHAR(50) | | 昵称 |
| created_at | DATETIME | | 创建时间 |
| updated_at | DATETIME | | 更新时间 |

---

## 4.2 News

新闻资讯。

| 字段 | 类型 | 约束 | 说明 |
|------|------|------|------|
| id | BIGINT | PK | 主键 |
| title | VARCHAR(200) | NOT NULL | 标题 |
| summary | VARCHAR(500) | | 摘要 |
| cover_image | VARCHAR(255) | | 封面图 |
| content | TEXT | | 正文 |
| publish_time | DATETIME | | 发布时间 |
| created_at | DATETIME | | 创建时间 |
| updated_at | DATETIME | | 更新时间 |

---

## 4.3 PageContent

页面内容。

用于后台维护官网静态内容。

| 字段 | 类型 | 约束 | 说明 |
|------|------|------|------|
| id | BIGINT | PK | 主键 |
| page_key | VARCHAR(100) | UNIQUE | 页面标识 |
| title | VARCHAR(200) | | 标题 |
| content | LONGTEXT | | 页面内容 |
| updated_at | DATETIME | | 更新时间 |

---

## 4.4 Product

产品信息。

| 字段 | 类型 | 约束 | 说明 |
|------|------|------|------|
| id | BIGINT | PK | 主键 |
| trace_code | VARCHAR(100) | UNIQUE | 溯源码 |
| name | VARCHAR(100) | | 产品名称 |
| category | VARCHAR(50) | | 产品类别 |
| batch_no | VARCHAR(100) | | 批次号 |
| image | VARCHAR(255) | | 产品图片 |
| report_file | VARCHAR(255) | | 检测报告 |
| created_at | DATETIME | | 创建时间 |
| updated_at | DATETIME | | 更新时间 |

---

## 4.5 TraceRecord

产品溯源时间轴。

| 字段 | 类型 | 约束 | 说明 |
|------|------|------|------|
| id | BIGINT | PK | 主键 |
| product_id | BIGINT | FK | 产品ID |
| title | VARCHAR(100) | | 节点标题 |
| description | TEXT | | 节点说明 |
| image | VARCHAR(255) | | 节点图片 |
| record_time | DATETIME | | 节点时间 |
| sort_order | INT | | 排序 |
| created_at | DATETIME | | 创建时间 |

---

# 5. 实体关系

## Product

一个产品：

- 一个溯源码
- 一个批次
- 多个溯源节点

---

## TraceRecord

一个节点：

- 属于一个产品
- 一个时间
- 一个标题
- 一张图片（可选）

多个节点组成完整时间轴。

---

# 6. 命名规范

数据表：

使用：

snake_case

例如：

news

trace_record

page_content

字段：

统一：

snake_case

例如：

trace_code

publish_time

created_at

updated_at

主键：

id

外键：

xxx_id

例如：

product_id

---

# 7. 索引规范

建立索引：

Product

- trace_code（唯一索引）

News

- publish_time

TraceRecord

- product_id
- record_time

PageContent

- page_key（唯一索引）

---

# 8. 数据完整性

必须：

- 主键唯一
- 外键保持一致
- 删除产品前应先处理关联记录
- 不允许孤立 TraceRecord

---

# 9. 审计字段

所有业务表统一包含：

created_at

updated_at

便于：

- 数据追踪
- 日志分析
- 后续扩展

---

# 10. 文件存储

数据库仅保存：

图片地址

PDF 地址

实际文件：

存储于对象存储或服务器文件系统。

禁止：

数据库存储图片二进制数据。

---

# 11. 未来扩展

V2：

新增：

- QRCode
- Batch

V3：

新增：

- Reservation
- Order
- Customer

V4：

新增：

- SensorData
- LiveStream
- Device
- EnvironmentRecord

以上新增不得破坏现有数据结构。

---

# 12. 数据库设计原则

遵循：

- Third Normal Form（3NF）
- Single Responsibility
- High Cohesion
- Low Coupling

避免：

- 冗余字段
- 重复数据
- 多值字段
- 一个字段存储多个业务含义

数据库设计应保持简单、清晰，并支持长期演进。