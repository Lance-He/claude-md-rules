# CLAUDE - Python 开发规范

This file provides guidance to Claude Code (claude.ai/code) when working with Python code in this repository.

### 第一部分：核心编程原则 (Guiding Principles)
这是我们合作的顶层思想，指导所有具体的行为。

#### 基础设计原则
- **可读性优先 (Readability First)：** 遵循 "The Zen of Python" - 代码应该像诗一样优美，简洁胜过复杂。
- **DRY (Don't Repeat Yourself)：** 通过函数、类、模块和装饰器来消除重复，充分利用 Python 的抽象能力。
- **高内聚，低耦合 (High Cohesion, Low Coupling)：** 利用 Python 的模块系统和包结构实现清晰的代码组织。

#### DDD + TDD 融合开发方法论
- **领域驱动设计 (Domain-Driven Design)：** 采用 Domain Model 并结合 Python 的类型注解，以业务领域为核心组织代码结构。
- **测试驱动开发 (Test-Driven Development)：** 使用 pytest 框架，每完成一个功能模块就立即编写相应的测试。
- **渐进式开发策略：** 利用 Python 的交互式特性，每写一个单元就在 REPL 或 Jupyter 中验证。
- **领域边界清晰：** 通过 Python 包和模块系统明确 domain 关系对应。
- **AI 辅助质量保障：** 结合 AI 工具和 Python 的静态分析工具（mypy、pylint）提升代码质量。

### 第二部分：具体执行指令 (Actionable Instructions)
这是 Claude 在 Python 开发中需要严格遵守的具体操作指南。

#### 沟通与语言规范
- **默认语言：** 请默认使用简体中文进行所有交流、解释和思考过程的陈述。
- **代码与术语：** 所有代码实体（变量名、函数名、类名等）及技术术语必须保持英文原文。
- **注释规范：** 代码注释应使用中文，遵循 PEP 257 文档字符串规范。
- **类型注解强制要求：** 所有函数和方法必须添加类型注解，提高代码可读性和IDE支持。

#### 批判性反馈与破框思维
- **审慎分析：** 必须以审视和批判的眼光分析输入，主动识别潜在的问题和 Pythonic 编程原则违背。
- **坦率直言：** 指出非 Pythonic 的代码模式，推荐更优雅的 Python 解决方案。
- **严厉质询：** 对于违背 PEP 规范或 Python 最佳实践的代码，必须明确指出并提供改进建议。

#### 开发与调试策略 (Development & Debugging Strategy)

##### 问题解决策略
- **坚韧不拔的解决问题：** 充分利用 Python 的调试工具（pdb、ipdb）和日志系统进行问题定位。
- **逐个击破：** 使用 Python 的交互式特性逐步验证每个组件的功能。
- **探索有效替代方案：** 优先考虑 Python 标准库和成熟的第三方库解决方案。
- **禁止伪造实现：** 严禁使用 `pass` 语句作为功能实现，所有代码必须具备真实逻辑。

##### 测试驱动开发 (TDD) 规范
- **pytest 优先原则：** 使用 pytest 作为主要测试框架，充分利用其 fixture 和参数化功能。
- **Red-Green-Refactor 循环：** 
  1. **Red（红）：** 编写失败的测试用例，使用 `pytest.raises` 验证异常情况
  2. **Green（绿）：** 编写最少的代码使测试通过
  3. **Refactor（重构）：** 利用 Python 的语法糖和内置函数优化代码
- **测试覆盖率：** 使用 coverage.py 确保测试覆盖率达到 90% 以上
- **doctest 集成：** 在文档字符串中包含可执行的示例代码

##### AI 辅助开发指导原则
- **静态分析集成：** 结合 mypy、pylint、black 等工具确保代码质量
- **IDE 增强：** 利用 AI 辅助的代码补全和重构建议
- **代码审查：** 对 AI 生成的代码进行 Pythonic 原则检查

#### Python 虚拟环境强制规范
- **虚拟环境必备：** 所有 Python 项目**必须**使用虚拟环境，推荐使用 `venv` 或 `conda`
- **环境管理：** 
  ```bash
  # 创建虚拟环境
  python -m venv venv
  # 激活虚拟环境
  source venv/bin/activate  # Linux/macOS
  .\venv\Scripts\activate   # Windows
  ```
- **依赖管理：** 使用 `requirements.txt` 或 `pyproject.toml` 管理项目依赖
- **环境隔离：** 严禁在全局环境中安装项目依赖

#### 项目与代码维护
- **PEP 规范遵循：** 严格遵守 PEP 8 代码风格，使用 black 进行代码格式化
- **文档字符串：** 遵循 PEP 257，为所有公共函数和类编写详细的文档字符串
- **导入排序：** 使用 isort 工具进行导入语句排序和分组
- **及时清理：** 定期清理未使用的导入和变量

## 常用命令

### 环境管理
```bash
# 创建虚拟环境
python -m venv venv

# 激活虚拟环境
source venv/bin/activate  # Linux/macOS
.\venv\Scripts\activate   # Windows

# 安装依赖
pip install -r requirements.txt

# 生成依赖文件
pip freeze > requirements.txt

# 使用 poetry 管理依赖
poetry init
poetry add package_name
poetry install
```

### 测试和质量检查
```bash
# 运行测试
pytest

# 运行测试并生成覆盖率报告
pytest --cov=src --cov-report=html

# 类型检查
mypy src/

# 代码格式化
black src/
isort src/

# 代码检查
pylint src/
flake8 src/
```

### 包管理
```bash
# 创建包结构
python -m src.module

# 构建包
python -m build

# 安装本地包
pip install -e .
```

## 项目架构概览

### 推荐项目结构
```
project/
├── src/
│   ├── domain/          # 领域模型
│   │   ├── entities/    # 实体类
│   │   ├── value_objects/ # 值对象
│   │   └── services/    # 领域服务
│   ├── application/     # 应用层
│   │   ├── use_cases/   # 用例
│   │   └── dtos/        # 数据传输对象
│   ├── infrastructure/  # 基础设施层
│   │   ├── repositories/ # 仓储实现
│   │   └── adapters/    # 适配器
│   └── interfaces/      # 接口层
│       └── web/         # Web 接口
├── tests/
│   ├── unit/           # 单元测试
│   ├── integration/    # 集成测试
│   └── e2e/           # 端到端测试
├── docs/              # 文档
├── requirements.txt   # 依赖管理
├── pyproject.toml    # 项目配置
└── README.md         # 项目说明
```

### 技术栈推荐
- **Web 框架：** FastAPI (异步) / Flask (同步) / Django (全栈)
- **ORM：** SQLAlchemy / Django ORM / Tortoise ORM
- **测试框架：** pytest + pytest-asyncio
- **类型检查：** mypy
- **代码格式化：** black + isort
- **代码检查：** pylint + flake8
- **文档生成：** Sphinx / MkDocs
- **异步编程：** asyncio + aiohttp

## 开发指南

### 领域驱动设计 (DDD) 实施指南

#### 领域模型组织
```python
# 实体示例
from dataclasses import dataclass
from typing import Optional
from uuid import UUID, uuid4

@dataclass
class User:
    id: UUID = None
    name: str
    email: str
    
    def __post_init__(self):
        if self.id is None:
            self.id = uuid4()
    
    def change_email(self, new_email: str) -> None:
        """更改用户邮箱"""
        if not self._is_valid_email(new_email):
            raise ValueError("Invalid email format")
        self.email = new_email
    
    def _is_valid_email(self, email: str) -> bool:
        """验证邮箱格式"""
        return "@" in email  # 简化实现
```

#### 值对象设计
```python
from dataclasses import dataclass
from typing import Protocol

@dataclass(frozen=True)
class Money:
    amount: float
    currency: str = "USD"
    
    def __post_init__(self):
        if self.amount < 0:
            raise ValueError("Amount cannot be negative")
    
    def add(self, other: 'Money') -> 'Money':
        if self.currency != other.currency:
            raise ValueError("Cannot add different currencies")
        return Money(self.amount + other.amount, self.currency)
```

#### 仓储模式
```python
from abc import ABC, abstractmethod
from typing import List, Optional

class UserRepository(ABC):
    @abstractmethod
    async def save(self, user: User) -> None:
        pass
    
    @abstractmethod
    async def find_by_id(self, user_id: UUID) -> Optional[User]:
        pass
    
    @abstractmethod
    async def find_by_email(self, email: str) -> Optional[User]:
        pass

class SQLUserRepository(UserRepository):
    def __init__(self, db_session):
        self.db_session = db_session
    
    async def save(self, user: User) -> None:
        # 实现数据库保存逻辑
        pass
```

### 测试驱动开发最佳实践

#### 单元测试示例
```python
import pytest
from src.domain.entities.user import User
from src.domain.value_objects.money import Money

class TestUser:
    def test_user_creation(self):
        user = User(name="张三", email="zhangsan@example.com")
        assert user.name == "张三"
        assert user.email == "zhangsan@example.com"
        assert user.id is not None
    
    def test_change_email_success(self):
        user = User(name="张三", email="zhangsan@example.com")
        user.change_email("new@example.com")
        assert user.email == "new@example.com"
    
    def test_change_email_invalid_format(self):
        user = User(name="张三", email="zhangsan@example.com")
        with pytest.raises(ValueError, match="Invalid email format"):
            user.change_email("invalid-email")

class TestMoney:
    def test_money_creation(self):
        money = Money(100.0, "USD")
        assert money.amount == 100.0
        assert money.currency == "USD"
    
    def test_money_add_same_currency(self):
        money1 = Money(100.0, "USD")
        money2 = Money(50.0, "USD")
        result = money1.add(money2)
        assert result.amount == 150.0
    
    def test_money_add_different_currency_raises_error(self):
        money1 = Money(100.0, "USD")
        money2 = Money(50.0, "EUR")
        with pytest.raises(ValueError, match="Cannot add different currencies"):
            money1.add(money2)
```

#### 集成测试示例
```python
import pytest
from src.application.use_cases.create_user import CreateUserUseCase
from src.infrastructure.repositories.sql_user_repository import SQLUserRepository

@pytest.mark.asyncio
async def test_create_user_use_case(db_session):
    repository = SQLUserRepository(db_session)
    use_case = CreateUserUseCase(repository)
    
    user_id = await use_case.execute("张三", "zhangsan@example.com")
    
    created_user = await repository.find_by_id(user_id)
    assert created_user is not None
    assert created_user.name == "张三"
    assert created_user.email == "zhangsan@example.com"
```

### 异步编程规范

#### 异步函数设计
```python
import asyncio
from typing import List
import aiohttp

async def fetch_user_data(user_id: int) -> dict:
    """异步获取用户数据"""
    async with aiohttp.ClientSession() as session:
        async with session.get(f"/api/users/{user_id}") as response:
            return await response.json()

async def process_users(user_ids: List[int]) -> List[dict]:
    """并发处理多个用户"""
    tasks = [fetch_user_data(user_id) for user_id in user_ids]
    return await asyncio.gather(*tasks)
```

### 错误处理和日志

#### 异常处理最佳实践
```python
import logging
from typing import Optional

logger = logging.getLogger(__name__)

class UserServiceError(Exception):
    """用户服务异常基类"""
    pass

class UserNotFoundError(UserServiceError):
    """用户未找到异常"""
    pass

class UserService:
    def __init__(self, repository: UserRepository):
        self.repository = repository
    
    async def get_user(self, user_id: UUID) -> User:
        try:
            user = await self.repository.find_by_id(user_id)
            if user is None:
                raise UserNotFoundError(f"User with id {user_id} not found")
            return user
        except Exception as e:
            logger.error(f"Error getting user {user_id}: {e}")
            raise UserServiceError(f"Failed to get user: {e}") from e
```

## 开发强制要求 ⚠️

1. **虚拟环境强制要求：** 所有 Python 项目必须使用虚拟环境
2. **类型注解强制要求：** 所有函数和方法必须添加类型注解
3. **测试覆盖率要求：** 核心业务逻辑测试覆盖率不低于 90%
4. **代码风格要求：** 必须通过 black、isort、pylint 检查
5. **文档字符串要求：** 所有公共函数和类必须有详细的文档字符串
6. **PEP 规范遵循：** 严格遵守 PEP 8 和相关 PEP 规范
7. **异步代码规范：** 异步函数必须使用 async/await 语法，不使用回调

## 工具链集成

### 开发环境配置
```bash
# 安装开发依赖
pip install pytest coverage mypy black isort pylint

# 创建 .pre-commit-config.yaml
repos:
  - repo: https://github.com/psf/black
    rev: 22.3.0
    hooks:
      - id: black
  - repo: https://github.com/pycqa/isort
    rev: 5.10.1
    hooks:
      - id: isort
  - repo: https://github.com/pycqa/pylint
    rev: v2.13.0
    hooks:
      - id: pylint
```

### VS Code 配置
```json
{
    "python.formatting.provider": "black",
    "python.linting.pylintEnabled": true,
    "python.linting.mypyEnabled": true,
    "python.testing.pytestEnabled": true,
    "python.testing.unittestEnabled": false,
    "python.testing.nosetestsEnabled": false
}
```

## 注意事项

- 充分利用 Python 的语法糖和内置函数
- 遵循 "Pythonic" 编程风格
- 优先使用标准库，谨慎选择第三方依赖
- 注意 Python 的 GIL 限制，CPU 密集型任务考虑多进程
- 合理使用异步编程，避免阻塞操作
- 重视代码的可读性和简洁性
- 定期更新依赖包，关注安全漏洞

这个规范强调了 Python 的优雅、简洁和可读性，同时保持了 DDD + TDD 的核心理念，为 Python 开发提供了全面的指导。
