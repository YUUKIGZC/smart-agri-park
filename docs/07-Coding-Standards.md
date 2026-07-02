# 智慧农业生态园官网
# Coding Standards（V1.0）

---

# 1. 文档说明

本文档定义项目统一编码规范。

目标：

- 保持代码风格一致
- 提高代码可读性
- 提高可维护性
- 便于多人协作
- 提高 AI Agent 生成代码质量

所有新增代码必须遵循本规范。

---

# 2. 总体原则

遵循：

- SOLID
- DRY（Don't Repeat Yourself）
- KISS（Keep It Simple）
- YAGNI（You Aren't Gonna Need It）
- Clean Code

优先保证：

正确性 > 可读性 > 可维护性 > 性能优化

MVP 阶段避免过度设计。

---

# 3. 文件组织

推荐结构：

```text
src/
├── components/
├── pages/
├── layouts/
├── services/
├── stores/
├── hooks/
├── utils/
├── assets/
└── types/
```

禁止将大量无关文件放在同一目录。

---

# 4. 命名规范

## 文件

组件：

PascalCase

例如：

HeroBanner

TraceTimeline

NewsCard

普通文件：

camelCase

例如：

newsService

dateUtil

---

## 变量

使用：

camelCase

例如：

newsList

traceCode

userInfo

禁止：

a

data1

temp

---

## 常量

全部大写：

```text
MAX_UPLOAD_SIZE

DEFAULT_PAGE_SIZE
```

---

## 数据库

统一：

snake_case

例如：

trace_record

page_content

---

# 5. 函数规范

一个函数：

只负责一件事情。

推荐：

20~50 行。

避免：

超过 100 行。

函数名必须体现行为。

例如：

```text
getNewsList()

createProduct()

deleteTraceRecord()
```

禁止：

```text
doData()

handle()

test()
```

---

# 6. 组件规范

组件职责单一。

一个组件：

一个主要功能。

超过 300 行应考虑拆分。

公共组件：

不得依赖业务逻辑。

业务组件：

可组合多个公共组件。

---

# 7. 页面规范

页面仅负责：

- 页面布局
- 数据请求
- 状态管理

复杂业务逻辑：

放入：

- Service
- Store
- Hook

禁止在页面中编写大量业务代码。

---

# 8. API 调用

所有 HTTP 请求统一封装。

禁止：

页面直接调用底层 HTTP 客户端。

统一通过：

services/

访问接口。

---

# 9. 状态管理

共享状态：

放入 Store。

页面局部状态：

使用组件自身状态。

避免：

层层 Props 传递。

---

# 10. 注释规范

代码应具有良好的可读性。

注释解释：

为什么（Why）

而不是：

做什么（What）

避免无意义注释：

```text
// 定义变量

const name = ...
```

公共组件、复杂函数应提供必要说明。

---

# 11. 错误处理

所有异常统一处理。

禁止：

空 catch。

禁止：

忽略异常。

错误信息应友好展示。

日志中保留详细异常信息。

---

# 12. 表单规范

所有输入：

必须校验。

包括：

- 必填
- 长度
- 格式
- 文件类型

禁止依赖前端校验。

后端必须再次验证。

---

# 13. Magic Number

禁止：

```text
if(status==3)
```

应定义：

```text
const STATUS_PUBLISHED = 3
```

所有业务值应具备明确含义。

---

# 14. 硬编码

禁止：

接口地址

角色名称

颜色值

配置参数

应统一放入：

- config
- constants
- environment

---

# 15. 样式规范

优先使用统一设计系统。

禁止：

页面随意定义颜色。

禁止：

随意定义间距。

统一使用：

Design System

中的：

颜色

字体

间距

圆角

阴影

---

# 16. 性能规范

图片：

按需加载。

长列表：

分页。

组件：

按需渲染。

避免：

重复请求。

避免：

重复渲染。

---

# 17. 安全规范

密码：

禁止明文存储。

Token：

禁止写入源码。

上传：

验证文件类型。

接口：

校验权限。

禁止：

SQL 注入。

禁止：

XSS。

---

# 18. Git Commit

统一格式：

```text
feat:

fix:

docs:

refactor:

style:

test:

chore:
```

例如：

```text
feat: add trace timeline page

fix: resolve mobile navbar overlap

docs: update API specification
```

禁止：

```text
update

修改

111

finally
```

---

# 19. AI Agent 开发规范

AI Agent 每次仅完成一个独立任务。

完成后必须：

- 保证可运行
- 无编译错误
- 无重复代码
- 符合 Design System
- 符合 Tech Spec
- 符合 Architecture
- 符合 API 规范

不得一次生成整个项目。

每完成一个任务，应等待 Review 后再继续。

---

# 20. Definition of Done（DoD）

一个任务只有满足以下条件才算完成：

- 功能开发完成
- 无编译错误
- 无明显 Bug
- 符合设计规范
- 符合编码规范
- 页面可正常访问
- 响应式布局正常
- 必要注释已补充
- Git 状态干净
- 可以进入下一任务

---

# 21. 文档维护

本规范适用于整个项目生命周期。

如编码规范发生调整，应及时更新本文档。

所有开发人员及 AI Agent 均应遵循本规范。