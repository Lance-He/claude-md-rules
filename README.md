# Claude 编程规范指南

一套全面的多语言编程规范指南，基于领域驱动设计（DDD）+ 测试驱动开发（TDD）+ AI 辅助开发的现代软件开发理念。

## 📖 项目简介

本项目为不同编程语言和技术栈提供统一而又针对性的开发规范，旨在：

- 提升代码质量和可维护性
- 统一团队开发标准
- 融合现代软件开发最佳实践
- 提供 AI 辅助开发指导

## 🏗️ 核心理念

### DDD + TDD + AI 融合开发方法论

- **领域驱动设计 (DDD)：** 以业务领域为核心组织代码结构
- **测试驱动开发 (TDD)：** Red-Green-Refactor 循环，确保代码质量
- **AI 辅助开发：** 利用 AI 工具提升开发效率，但保持人工质量把控

### 统一原则

- **可读性优先：** 代码是写给人看的
- **DRY 原则：** 通过抽象消除重复
- **高内聚，低耦合：** 模块化设计
- **渐进式开发：** 小步快跑，持续反馈

## 📁 项目结构

```
Claude-Rules/
├── README.md                         # 项目介绍
├── GENERAL_DEVELOPMENT_STANDARDS.md  # 通用开发标准（语言无关）
├── Java/
│   └── CLAUDE.md                    # Java 开发规范
├── Python/
│   └── CLAUDE.md                    # Python 开发规范
├── C/
│   └── CLAUDE.md                    # C 语言开发规范
└── Frontend/
    └── CLAUDE.md                    # 前端开发规范
```

## 🎯 通用开发标准

在查看具体语言规范之前，建议先阅读 [通用开发标准](GENERAL_DEVELOPMENT_STANDARDS.md)，它包含了所有编程语言通用的：

- 核心编程原则
- 开发流程规范
- 代码质量标准
- 项目结构建议
- 测试和文档规范
- 团队协作指南

## 🚀 语言规范概览

### 🔥 Java 规范
**适用场景：** 企业级应用、微服务架构、Spring Boot 项目

**核心特色：**
- Spring Boot 3.5.0 + Java 17 技术栈
- 分层架构（Controller-Service-Mapper）
- Sa-Token 权限验证强制要求
- MyBatis Plus + Redis 数据层
- 插件化架构设计

**强制要求：**
- 构造器注入（`@RequiredArgsConstructor`）
- 权限验证（`@SaCheckPermission`）
- 统一路径前缀（`/coder`）

### 🐍 Python 规范
**适用场景：** Web 应用、数据科学、AI/ML 项目、脚本工具

**核心特色：**
- Pythonic 编程风格
- 虚拟环境强制使用
- 类型注解（Type Hints）
- pytest 测试框架
- 异步编程（asyncio）支持

**强制要求：**
- 虚拟环境：`python -m venv venv`
- 类型注解：所有函数必须有类型标注
- PEP 规范：PEP 8 + PEP 257
- 测试覆盖率：90% 以上

### ⚡ C 语言规范
**适用场景：** 系统编程、嵌入式开发、性能敏感应用

**核心特色：**
- 内存安全优先
- RAII 思想应用
- 模块化设计（.h/.c）
- 静态分析工具集成
- 跨平台兼容性

**强制要求：**
- 内存管理：每个 malloc 对应 free
- 边界检查：防止缓冲区溢出
- 静态分析：Clang Static Analyzer + Valgrind
- 编译警告：-Wall -Wextra 零容忍

### 🌐 前端规范
**适用场景：** Web 应用、移动端 H5、桌面应用（Electron）

**核心特色：**
- 用户体验优先
- TypeScript 强制要求
- 组件化开发
- 现代构建工具链
- 可访问性（A11y）支持

**强制要求：**
- TypeScript：禁止使用 `any` 类型
- 测试覆盖率：组件测试 80% 以上
- 可访问性：WCAG 2.1 标准
- 性能指标：首屏 < 3s，LCP < 2.5s

## 🛠️ 使用方法

### 1. 选择对应的语言规范

根据你的项目技术栈，选择相应的规范文档：

```bash
# Java 项目
cp Java/CLAUDE.md /path/to/your/java/project/

# Python 项目
cp Python/CLAUDE.md /path/to/your/python/project/

# C 项目
cp C/CLAUDE.md /path/to/your/c/project/

# 前端项目
cp Frontend/CLAUDE.md /path/to/your/frontend/project/
```

### 2. 配置开发环境

每个规范文档都包含详细的开发环境配置指南，包括：

- 工具链安装
- 代码格式化配置
- 测试框架设置
- CI/CD 集成

### 3. 遵循开发流程

按照规范中的 TDD 流程进行开发：

1. **Red（红）：** 先写失败的测试
2. **Green（绿）：** 编写最少代码使测试通过
3. **Refactor（重构）：** 优化代码结构

## 📊 规范对比

| 特性 | Java | Python | C | Frontend |
|------|------|--------|---|----------|
| **框架** | Spring Boot | FastAPI/Django | 无/自建 | React/Vue/Angular |
| **测试框架** | JUnit + Mockito | pytest | Unity/CUnit | Jest + Testing Library |
| **包管理** | Maven/Gradle | pip/poetry | Make/CMake | npm/yarn/pnpm |
| **代码风格** | Checkstyle | black + isort | clang-format | ESLint + Prettier |
| **类型系统** | 静态类型 | 类型注解 | 静态类型 | TypeScript |
| **内存管理** | 自动（GC） | 自动（GC） | 手动 | 自动（GC） |

## 🎯 最佳实践示例

### Java 示例
```java
@RestController
@RequestMapping("/coder/user")
@RequiredArgsConstructor
public class UserController {
    
    private final UserService userService;
    
    @SaCheckPermission("user:list")
    @GetMapping("/list")
    public Result<List<User>> list(@Validated UserBo bo) {
        return Result.ok(userService.list(bo));
    }
}
```

### Python 示例
```python
from typing import List
import pytest

async def fetch_users() -> List[User]:
    """获取用户列表"""
    async with aiohttp.ClientSession() as session:
        async with session.get("/api/users") as response:
            return await response.json()

@pytest.mark.asyncio
async def test_fetch_users():
    users = await fetch_users()
    assert len(users) > 0
```

### C 示例
```c
// user.h
typedef struct User {
    uint32_t id;
    char name[64];
    char email[128];
} User;

UserResult user_create(User** user, const char* name, const char* email);
void user_destroy(User* user);
```

### Frontend 示例
```typescript
interface UserProps {
  user: User;
  onEdit?: (user: User) => void;
}

const UserCard: React.FC<UserProps> = ({ user, onEdit }) => {
  return (
    <div role="article" aria-label={`用户 ${user.name} 的信息`}>
      <h3>{user.name}</h3>
      <p>{user.email}</p>
      {onEdit && (
        <button onClick={() => onEdit(user)}>
          编辑
        </button>
      )}
    </div>
  );
};
```

## 🤝 贡献指南

欢迎贡献改进建议！请遵循以下步骤：

1. Fork 本仓库
2. 创建特性分支：`git checkout -b feature/your-feature`
3. 提交修改：`git commit -m 'Add some feature'`
4. 推送分支：`git push origin feature/your-feature`
5. 创建 Pull Request

### 贡献方向

- 新增语言规范（Go、Rust、Kotlin 等）
- 完善现有规范的最佳实践
- 添加更多代码示例
- 改进工具链集成
- 翻译成其他语言

## 📜 版本历史

- **v1.0.0** - 初始版本，包含 Java、Python、C、Frontend 四种规范
- **v1.1.0** - 完善 DDD + TDD 融合方法论
- **v1.2.0** - 新增 AI 辅助开发指导原则

## 📄 许可证

本项目采用 [MIT 许可证](LICENSE)。

## 📧 联系方式

如有问题或建议，请通过以下方式联系：

- 创建 [Issue](https://github.com/Lance-He/Claude-Rules/issues)
- 发送邮件至：hesiqi.china@gmail.com

## 🙏 致谢

感谢所有为现代软件开发实践做出贡献的开发者和社区，特别是：

- Domain-Driven Design 社区
- Test-Driven Development 推广者
- 各语言生态系统的维护者
- AI 辅助开发工具的创新者

---

**让我们一起构建更高质量的软件！** 🚀