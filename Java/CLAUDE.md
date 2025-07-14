# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

### 第一部分：核心编程原则 (Guiding Principles)
这是我们合作的顶层思想，指导所有具体的行为。

#### 基础设计原则
- **可读性优先 (Readability First)：** 始终牢记"代码是写给人看的，只是恰好机器可以执行"。清晰度高于一切。
- **DRY (Don't Repeat Yourself)：** 绝不复制代码片段。通过抽象（如函数、类、模块）来封装和复用通用逻辑。
- **高内聚，低耦合 (High Cohesion, Low Coupling)：** 功能高度相关的代码应该放在一起（高内聚），而模块之间应尽量减少依赖（低耦合），以增强模块独立性和可维护性。

#### DDD + TDD 融合开发方法论
- **领域驱动设计 (Domain-Driven Design)：** 采用 Domain Model（领域模型）并结合 SOLID 设计原则，以业务领域为核心组织代码结构。
- **测试驱动开发 (Test-Driven Development)：** 每完成一个功能模块就立即编写相应的测试，确保代码质量和稳定性。
- **渐进式开发策略：** 每写一个单元就进行一轮测试，避免后期全局修改和发现系统性问题。
- **领域边界清晰：** 通过明确的 domain 关系对应，减少设计偏差和架构混乱。
- **AI 辅助质量保障：** 结合 AI 工具提升软件设计和技术管理的标准，但核心的设计决策和质量把控仍需人工判断。

### 第二部分：具体执行指令 (Actionable Instructions)
这是 Claude 在日常工作中需要严格遵守的具体操作指南。
沟通与语言规范
默认语言：请默认使用简体中文进行所有交流、解释和思考过程的陈述。
代码与术语：所有代码实体（变量名、函数名、类名等）及技术术语（如库名、框架名、设计模式等）必须保持英文原文。
注释规范：代码注释应使用中文。
行尾注释禁令 (End-of-Line Comment Prohibition)：严格禁止在代码行末尾添加注释（如 `code; // 注释`）。所有注释必须单独占行或作为方法/类的头部注释。这确保代码的简洁性和可读性，避免行尾注释造成的视觉干扰。
批判性反馈与破框思维 (Critical Feedback & Out-of-the-Box Thinking)：
审慎分析：必须以审视和批判的眼光分析我的输入，主动识别潜在的问题、逻辑谬误或认知偏差。
坦率直言：需要明确、直接地指出我思考中的盲点，并提供显著超越我当前思考框架的建议，以挑战我的预设。
严厉质询 (Tough Questioning)：当我提出的想法或方案明显不合理、过于理想化或偏离正轨时，必须使用更直接、甚至尖锐的言辞进行反驳和质询，帮我打破思维定式，回归理性。
开发与调试策略 (Development & Debugging Strategy)

#### 问题解决策略
- **坚韧不拔的解决问题 (Tenacious Problem-Solving)：** 当面对编译错误、逻辑不通或多次尝试失败时，绝不允许通过简化或伪造实现来"绕过"问题。
- **逐个击破 (Incremental Debugging)：** 必须坚持对错误和问题进行逐一分析、定位和修复。
- **探索有效替代方案 (Explore Viable Alternatives)：** 如果当前路径确实无法走通，应切换到另一个逻辑完整、功能健全的替代方案来解决问题，而不是退回到一个简化的、虚假的版本。
- **禁止伪造实现 (No Fake Implementations)：** 严禁使用占位符逻辑（如空的循环）、虚假数据或不完整的函数来伪装功能已经实现。所有交付的代码都必须是意图明确且具备真实逻辑的。
- **战略性搁置 (Strategic Postponement)：** 只有当一个问题被证实非常困难，且其当前优先级不高时，才允许被暂时搁置。搁置时，必须以 TODO 形式在代码中或任务列表中明确标记，并清晰说明遇到的问题。在核心任务完成后，必须回过头来重新审视并解决这些被搁置的问题。

#### 测试驱动开发 (TDD) 规范
- **Red-Green-Refactor 循环：** 严格遵循 TDD 的核心流程：
  1. **Red（红）：** 先编写一个失败的测试用例
  2. **Green（绿）：** 编写最少的代码使测试通过
  3. **Refactor（重构）：** 在保持测试通过的前提下优化代码结构
- **测试优先原则：** 在编写任何功能代码之前，必须先编写对应的测试用例
- **小步快跑：** 每次只添加一个小功能，立即编写测试，确保每个迭代都有测试覆盖
- **持续反馈：** 每完成一个功能单元就运行全套测试，及时发现和修复问题
- **测试作为文档：** 测试用例应该清晰地表达业务需求和预期行为，成为活的文档
- **规范化测试文件管理 (Standardized Test File Management)：** 严禁为新功能在根目录或不相关位置创建孤立的测试文件。在添加测试时，必须首先检查项目中已有的测试套件（通常位于 tests/ 目录下），并将新的测试用例整合到与被测模块最相关的现有测试文件中。只有当确实没有合适的宿主文件时，才允许在 tests/ 目录下创建符合项目命名规范的新测试文件。
#### AI 辅助开发指导原则
- **AI 工具定位：** AI 应作为开发效率的倍增器，而非替代开发者的决策能力。AI 擅长代码生成、重构建议和错误检测，但核心的架构设计和业务逻辑判断仍需人工把控。
- **质量标准提升：** 使用 AI 辅助开发要求更高的软件设计和技术管理标准，因为 AI 生成的代码需要更严格的审查和验证。
- **代码审查强化：** 对 AI 生成的代码必须进行全面的人工审查，特别关注业务逻辑的正确性、安全性和性能表现。
- **持续学习：** 开发者应该从 AI 的建议中学习最佳实践，同时教会 AI 项目特定的约定和模式。
- **工具链整合：** 将 AI 工具有机集成到现有的开发流程中，包括代码补全、测试生成、文档编写等环节。

项目与代码维护 (Project & Code Maintenance)
- **统一文档维护 (Unified Documentation Maintenance)：** 严禁为每个独立任务（如重构、功能实现）创建新的总结文档（例如 CODE_REFACTORING_SUMMARY.md）。在任务完成后，必须优先检查项目中已有的相关文档（如 README.md、既有的设计文档等），并将新的总结、变更或补充内容直接整合到现有文档中，维护其完整性和时效性。
- **及时清理 (Timely Cleanup)：** 在完成开发任务时，如果发现任何已无用（过时）的代码、文件或注释，应主动提出清理建议。

## 常用命令

### 构建和运行
```bash
# 编译整个项目
mvn clean compile

# 打包项目
mvn clean package

# 运行应用程序
cd coder-common-thin-web
mvn spring-boot:run

# 或者运行打包后的jar
java -jar coder-common-thin-web/target/coder-common-thin-web-1.0.0.jar
```

### 测试
```bash
# 运行所有测试
mvn test

# 运行单个模块测试
mvn test -pl coder-common-thin-web
```

### 数据库
```bash
# 数据库初始化SQL位于
# sql/coder-common-thin.sql
```

## 项目架构概览

这是一个基于Spring Boot 3.5.0的多模块企业级开发框架，采用插件化架构设计。

### 模块结构
- **coder-common-thin-web**: Web启动模块，应用程序入口点
- **coder-common-thin-common**: 公共工具模块，包含大量工具类、配置类和拦截器
- **coder-common-thin-model**: 数据模型模块，包含POJO、BO、VO和数据验证
- **coder-common-thin-mybatisplus**: 数据访问层模块，MyBatis Plus配置和Mapper
- **coder-common-thin-modules**: 业务模块容器
- **coder-common-thin-plugins**: 插件模块，包含各种功能插件

### 插件化架构
项目采用@Enable注解实现功能模块的可插拔配置：
- `@EnableCoderSaToken`: Sa-Token认证插件
- `@EnableCoderEasyExcel`: Excel处理插件
- `@EnableCoderLimit`: 限流插件
- `@EnableCoderRepeatSubmit`: 防重提交插件
- `@EnableCoderDesensitize`: 数据脱敏插件

### 技术栈
- **核心框架**: Spring Boot 3.5.0 + Java 17
- **数据库**: MySQL 9.3.0 + MyBatis Plus 3.5.12
- **缓存**: Redis（Spring Data Redis）
- **安全认证**: Sa-Token 1.43.0
- **工具库**: Hutool 5.8.38, Fastjson2 2.0.57, Guava 33.4.8
- **业务功能**: EasyExcel 4.0.3, Easy-Captcha 1.6.2

### 数据层设计
- **主键策略**: 雪花算法（ASSIGN_ID）
- **逻辑删除**: 0-已删除, 1-未删除
- **多数据源**: 支持master/slave数据源动态切换
- **SQL监控**: 集成P6spy进行SQL性能监控

### 配置文件
- **主配置**: `application.yml`
- **环境配置**: `application-dev.yml`
- **数据库配置**: 支持MySQL主从配置
- **Redis配置**: 使用Jackson2序列化，支持连接池

## 开发指南

### 添加新功能插件
1. 在`coder-common-thin-plugins`下创建新模块
2. 创建@Enable注解用于启用插件
3. 实现必要的配置类和工具类
4. 在主启动类上使用@Enable注解启用

### 数据访问层开发
1. 实体类放在`coder-common-thin-model/domain/pojo`
2. Mapper接口放在`coder-common-thin-mybatisplus/mapper`
3. XML映射文件放在`resources/mapper`
4. 使用`@DS("dataSourceName")`注解切换数据源

### 业务层开发规范
1. **依赖注入规范**: 所有ServiceImpl实现类必须使用`@RequiredArgsConstructor`构造器注入模式，禁止使用`@Autowired`字段注入
   - 在类上添加`@RequiredArgsConstructor`注解
   - 将需要注入的依赖声明为`private final`字段
   - Spring会自动通过构造器注入依赖

2. **Service分层规范**: Service层必须按功能模块分目录组织，不允许使用单一的impl目录
   - 每个功能模块创建独立目录（如：courseselection、courseoffering、coursecart）
   - 在各功能目录下放置对应的Service接口和ServiceImpl实现类
   - 包路径示例：`org.leocoder.course.education.service.courseselection.SysCourseSelectionService`

3. **Controller路径规范**: 所有Controller必须使用统一的`/coder`前缀作为API根路径
   - 所有Controller的`@RequestMapping`必须以`/coder`开头
   - 路径格式：`/coder/模块名/功能名`
   - 示例路径：`/coder/education/selection`、`/coder/education/offering`、`/coder/education/cart`
   - 参考示例：`@RequestMapping("/coder/education/selection")`

4. **Controller权限验证规范**: 所有Controller的接口方法必须配置权限验证
   - **强制要求**: 每个Controller方法都必须添加`@SaCheckPermission`注解
   - **导入依赖**: 在Controller类中导入`import cn.dev33.satoken.annotation.SaCheckPermission;`
   - **权限命名规范**: 使用格式`模块名:功能名:操作名`
      - 教育模块示例：`@SaCheckPermission("education:selection:list")`
      - 系统模块示例：`@SaCheckPermission("system:user:list")`
   - **操作名对应关系**:
      - `list` - 查询列表
      - `page` - 分页查询
      - `detail` - 查询详情
      - `add` - 新增
      - `edit` - 修改
      - `delete` - 删除
      - `status` - 状态变更
      - `import` - 导入
      - `export` - 导出
   - **示例代码**:
     ```java
     @RestController
     @RequestMapping("/coder/education/selection")
     public class SysCourseSelectionController {
         
         @SaCheckPermission("education:selection:list")
         @GetMapping("/list")
         public List<SysCourseSelection> list(@Validated CourseSelectionBo bo) {
             // 业务逻辑
         }
         
         @SaCheckPermission("education:selection:add")
         @PostMapping("/add")
         public String add(@Validated CourseSelectionBo bo) {
             // 业务逻辑
         }
     }
     ```
   - **禁止行为**:
      - 严禁创建没有权限验证的Controller方法
      - 严禁在Sa-Token配置中添加业务接口的排除路径
      - 严禁通过其他方式绕过权限验证

### 领域驱动设计 (DDD) 实施指南

#### 领域模型组织
- **领域边界划分：** 根据业务领域划分有界上下文（Bounded Context），每个上下文内部保持概念的一致性
- **领域对象设计：** 
  - **实体 (Entity)：** 具有唯一标识的业务对象，位于 `coder-common-thin-model/domain/pojo`
  - **值对象 (Value Object)：** 无标识的不可变对象，通过属性值判断相等性
  - **聚合根 (Aggregate Root)：** 作为聚合的入口点，确保业务规则的一致性
  - **领域服务 (Domain Service)：** 封装无法归属到特定实体的业务逻辑

#### 分层架构实现
- **应用层 (Application Layer)：** Controller 层，处理用户请求，协调领域对象完成业务用例
- **领域层 (Domain Layer)：** Service 层，包含核心业务逻辑和领域规则
- **基础设施层 (Infrastructure Layer)：** Mapper 层，提供数据持久化和外部系统集成
- **按领域模块组织：** Service 层按功能模块分目录组织，体现领域边界

#### 统一语言 (Ubiquitous Language)
- **命名一致性：** 代码中的类名、方法名、变量名应与业务术语保持一致
- **权限命名规范：** 使用 `模块名:功能名:操作名` 格式，体现业务领域结构
- **文档同步：** 确保代码、文档和业务人员使用相同的术语

#### 领域事件处理
- **事件驱动架构：** 通过领域事件实现不同聚合之间的松耦合通信
- **事件存储：** 记录重要的业务事件，支持事件溯源和审计
- **异步处理：** 对于复杂的业务流程，使用异步事件处理提高系统性能

### 工具类使用
项目提供了丰富的工具类，位于`coder-common-thin-common/utils`：
- **缓存工具**: `RedisUtil`, `LocalCacheUtil`
- **日期工具**: `DateUtil`, `CalendarUtil`
- **文件工具**: `FileUtil`, `UploadUtil`, `ZipUtil`
- **字符串工具**: `StringUtil`, `ConvertUtil`
- **IP工具**: `IpUtil`, `IpAddressUtil`
- **JSON工具**: `JsonUtil`
- **加密工具**: `MD5Util`, `CoderPasswordUtil`

### 配置说明
- **端口**: 默认18099，可通过`port`环境变量覆盖
- **文件路径**: 在`application-dev.yml`中配置`coder.filePath`
- **数据库连接**: 在`application-dev.yml`中配置数据源信息
- **Redis配置**: 在`application-dev.yml`中配置Redis连接信息

### 日志配置
- **日志文件**: `logback-spring.xml`
- **日志级别**: 可通过环境变量调整
- **操作日志**: 自动记录，支持异步处理和定时清理

## 注意事项

- 项目基于Java 17，确保开发环境版本匹配
- 使用中文注释，保持代码风格一致
- 新增功能遵循插件化设计模式
- 数据库操作优先使用MyBatis Plus提供的方法
- 安全认证统一使用Sa-Token，避免重复造轮子
- 工具类使用前先检查是否已有现成实现

## 重要规范文档

- 所有Controller必须配置权限验证（强制要求）
- 使用统一的路径前缀和权限命名规范
- 遵循标准的代码结构和注解使用规范

## 开发强制要求 ⚠️

1. **权限验证强制要求**: 任何新增的Controller方法都必须添加 `@SaCheckPermission` 注解
2. **禁止绕过权限验证**: 严禁通过排除路径或其他方式绕过Sa-Token权限验证
3. **权限命名标准化**: 必须使用 `模块名:功能名:操作名` 格式命名权限
4. **构造器注入**: 必须使用 `@RequiredArgsConstructor` 模式，禁用 `@Autowired`
5. **模块依赖管理**: 新增业务模块时必须在Web启动模块（`coder-course-web`）的pom.xml中添加对应依赖
   - **依赖检查原则**: 当Controller接口报错被当作静态资源处理时，首先检查Web模块是否缺少对应业务模块的依赖
   - **依赖添加规范**: 在`coder-course-web/pom.xml`中添加业务模块依赖，确保Spring Boot能扫描到所有Controller
   - **示例依赖配置**:
     ```xml
     <!-- 学生选课管理系统模块 -->
     <dependency>
         <groupId>org.leocoder.course</groupId>
         <artifactId>coder-course-education</artifactId>
         <version>${revision}</version>
     </dependency>
     ```
   - **验证方法**: 添加依赖后重新编译和启动应用程序，确保所有Controller接口能正常访问