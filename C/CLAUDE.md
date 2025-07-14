# CLAUDE.md - C 语言开发规范

This file provides guidance to Claude Code (claude.ai/code) when working with C code in this repository.

### 第一部分：核心编程原则 (Guiding Principles)
这是我们合作的顶层思想，指导所有具体的行为。

#### 基础设计原则
- **可读性优先 (Readability First)：** C 代码虽然接近硬件，但仍需保持清晰的结构和命名，每个函数只做一件事。
- **DRY (Don't Repeat Yourself)：** 通过函数、宏和模块化设计避免代码重复。
- **高内聚，低耦合 (High Cohesion, Low Coupling)：** 通过头文件和模块化设计实现清晰的接口分离。

#### 内存安全优先原则
- **内存管理严格化：** 每个 `malloc` 必须有对应的 `free`，使用 RAII 思想管理资源。
- **指针安全使用：** 避免野指针、空指针解引用和缓冲区溢出。
- **边界检查：** 所有数组访问和字符串操作都要进行边界检查。

#### DDD + TDD 融合开发方法论（C 语言适配）
- **模块化领域设计：** 通过 C 的模块系统（.h/.c 文件）实现领域边界划分。
- **结构化测试驱动：** 使用 Unity 或 CUnit 测试框架，每个函数都要有对应的测试。
- **渐进式开发策略：** 每完成一个模块立即进行单元测试和集成测试。
- **接口清晰化：** 通过头文件定义清晰的模块接口，隐藏实现细节。
- **AI 辅助安全检查：** 结合静态分析工具（Clang Static Analyzer、Valgrind）确保代码安全。

### 第二部分：具体执行指令 (Actionable Instructions)
这是 Claude 在 C 语言开发中需要严格遵守的具体操作指南。

#### 沟通与语言规范
- **默认语言：** 请默认使用简体中文进行所有交流、解释和思考过程的陈述。
- **代码与术语：** 所有代码实体（变量名、函数名、结构体名等）必须使用英文，遵循 C 语言命名约定。
- **注释规范：** 代码注释使用中文，函数头部必须有详细的注释说明。
- **编码标准：** 严格遵循 C99 或 C11 标准，避免使用编译器特定的扩展。

#### 批判性反馈与破框思维
- **安全性审查：** 对所有代码进行内存安全和缓冲区溢出检查。
- **性能意识：** 关注代码的时间复杂度和空间复杂度，避免不必要的内存分配。
- **可移植性检查：** 确保代码在不同平台和编译器上都能正确运行。

#### 开发与调试策略 (Development & Debugging Strategy)

##### 内存管理策略
- **RAII 思想应用：** 每个资源的获取都要有对应的释放机制。
- **内存泄漏预防：** 使用 Valgrind 检测内存泄漏，确保所有动态分配的内存都被释放。
- **缓冲区溢出预防：** 使用 `strncpy` 而非 `strcpy`，使用 `snprintf` 而非 `sprintf`。
- **指针使用规范：** 指针使用后立即置为 NULL，避免野指针。

##### 错误处理策略
- **返回值检查：** 所有函数的返回值都必须检查，特别是内存分配和文件操作。
- **错误码统一：** 定义统一的错误码系统，便于调试和维护。
- **异常安全：** 在发生错误时确保资源正确释放。

##### 测试驱动开发 (TDD) 规范
- **单元测试框架：** 使用 Unity 或 CUnit 作为测试框架。
- **测试用例设计：** 
  1. **边界条件测试：** 测试数组边界、空指针、极值情况
  2. **内存测试：** 测试内存分配失败的情况
  3. **功能测试：** 验证函数的核心功能
- **持续集成：** 每次代码提交都要通过所有测试用例。

##### AI 辅助开发指导原则
- **静态分析集成：** 使用 Clang Static Analyzer、Cppcheck 进行代码质量检查。
- **动态分析：** 使用 Valgrind、AddressSanitizer 检测运行时错误。
- **代码审查：** 对 AI 生成的代码进行安全性和性能审查。

#### 项目与代码维护
- **代码风格一致性：** 使用 clang-format 统一代码格式。
- **文档维护：** 每个模块都要有详细的设计文档和API文档。
- **版本控制：** 使用 Git 管理代码，合理使用分支策略。

## 常用命令

### 编译和构建
```bash
# 编译单个文件
gcc -std=c11 -Wall -Wextra -g -o program main.c

# 编译多个文件
gcc -std=c11 -Wall -Wextra -g -o program main.c module1.c module2.c

# 使用 Makefile
make clean
make all
make test

# 使用 CMake
mkdir build
cd build
cmake ..
make

# 静态库创建
ar rcs libmylib.a module1.o module2.o

# 动态库创建
gcc -shared -fPIC -o libmylib.so module1.c module2.c
```

### 调试和分析
```bash
# GDB 调试
gdb ./program
# 设置断点
(gdb) break main
# 运行程序
(gdb) run
# 单步执行
(gdb) step
# 查看变量
(gdb) print variable_name

# Valgrind 内存检查
valgrind --leak-check=full ./program

# AddressSanitizer 编译选项
gcc -fsanitize=address -g -o program main.c

# 静态分析
clang-static-analyzer main.c
cppcheck --enable=all main.c
```

### 测试
```bash
# 编译测试
gcc -std=c11 -Wall -Wextra -g -o test_program test_main.c unity.c src/*.c

# 运行测试
./test_program

# 测试覆盖率
gcc --coverage -o test_program test_main.c unity.c src/*.c
./test_program
gcov test_main.c
```

## 项目架构概览

### 推荐项目结构
```
project/
├── src/
│   ├── domain/          # 领域模块
│   │   ├── entities/    # 实体相关
│   │   ├── services/    # 领域服务
│   │   └── common/      # 通用工具
│   ├── infrastructure/ # 基础设施
│   │   ├── persistence/ # 数据持久化
│   │   └── network/     # 网络通信
│   └── interfaces/      # 接口层
├── include/            # 头文件
│   ├── domain/
│   ├── infrastructure/
│   └── interfaces/
├── tests/              # 测试文件
│   ├── unit/          # 单元测试
│   ├── integration/   # 集成测试
│   └── framework/     # 测试框架
├── docs/              # 文档
├── build/             # 构建输出
├── Makefile          # 构建脚本
├── CMakeLists.txt    # CMake 配置
└── README.md         # 项目说明
```

### 技术栈推荐
- **编译器：** GCC 9+ / Clang 10+
- **构建系统：** Make / CMake
- **测试框架：** Unity / CUnit / Check
- **调试工具：** GDB / LLDB
- **内存检查：** Valgrind / AddressSanitizer
- **静态分析：** Clang Static Analyzer / Cppcheck
- **代码格式：** clang-format
- **文档生成：** Doxygen

## 开发指南

### 模块化设计（DDD 在 C 语言中的实现）

#### 领域实体设计
```c
// user.h - 用户实体
#ifndef USER_H
#define USER_H

#include <stdbool.h>
#include <stdint.h>

typedef struct {
    uint32_t id;
    char name[64];
    char email[128];
    bool is_active;
} User;

typedef enum {
    USER_SUCCESS,
    USER_INVALID_EMAIL,
    USER_MEMORY_ERROR,
    USER_NOT_FOUND
} UserResult;

// 用户操作接口
UserResult user_create(User** user, const char* name, const char* email);
UserResult user_change_email(User* user, const char* new_email);
void user_destroy(User* user);
bool user_is_valid_email(const char* email);

#endif // USER_H
```

```c
// user.c - 用户实体实现
#include "user.h"
#include <stdlib.h>
#include <string.h>
#include <regex.h>

UserResult user_create(User** user, const char* name, const char* email) {
    if (!user || !name || !email) {
        return USER_INVALID_EMAIL;
    }
    
    if (!user_is_valid_email(email)) {
        return USER_INVALID_EMAIL;
    }
    
    *user = malloc(sizeof(User));
    if (!*user) {
        return USER_MEMORY_ERROR;
    }
    
    (*user)->id = 0; // 将由仓储层分配
    strncpy((*user)->name, name, sizeof((*user)->name) - 1);
    (*user)->name[sizeof((*user)->name) - 1] = '\0';
    
    strncpy((*user)->email, email, sizeof((*user)->email) - 1);
    (*user)->email[sizeof((*user)->email) - 1] = '\0';
    
    (*user)->is_active = true;
    
    return USER_SUCCESS;
}

UserResult user_change_email(User* user, const char* new_email) {
    if (!user || !new_email) {
        return USER_INVALID_EMAIL;
    }
    
    if (!user_is_valid_email(new_email)) {
        return USER_INVALID_EMAIL;
    }
    
    strncpy(user->email, new_email, sizeof(user->email) - 1);
    user->email[sizeof(user->email) - 1] = '\0';
    
    return USER_SUCCESS;
}

void user_destroy(User* user) {
    if (user) {
        free(user);
    }
}

bool user_is_valid_email(const char* email) {
    if (!email) return false;
    
    // 简化的邮箱验证逻辑
    const char* at_pos = strchr(email, '@');
    const char* dot_pos = strrchr(email, '.');
    
    return at_pos && dot_pos && (at_pos < dot_pos) && 
           (strlen(email) < 128) && (strlen(email) > 5);
}
```

#### 仓储模式实现
```c
// user_repository.h - 用户仓储接口
#ifndef USER_REPOSITORY_H
#define USER_REPOSITORY_H

#include "user.h"

typedef struct UserRepository UserRepository;

typedef struct {
    UserResult (*save)(UserRepository* repo, User* user);
    UserResult (*find_by_id)(UserRepository* repo, uint32_t id, User** user);
    UserResult (*find_by_email)(UserRepository* repo, const char* email, User** user);
    void (*destroy)(UserRepository* repo);
} UserRepositoryInterface;

typedef struct UserRepository {
    UserRepositoryInterface* interface;
    void* data; // 具体实现的数据
} UserRepository;

// 工厂函数
UserRepository* user_repository_create_memory(void);
UserRepository* user_repository_create_file(const char* filename);

#endif // USER_REPOSITORY_H
```

### 测试驱动开发示例

#### 单元测试
```c
// test_user.c - 用户单元测试
#include "unity.h"
#include "../src/domain/entities/user.h"

void setUp(void) {
    // 测试设置
}

void tearDown(void) {
    // 测试清理
}

void test_user_create_success(void) {
    User* user = NULL;
    UserResult result = user_create(&user, "张三", "zhangsan@example.com");
    
    TEST_ASSERT_EQUAL(USER_SUCCESS, result);
    TEST_ASSERT_NOT_NULL(user);
    TEST_ASSERT_EQUAL_STRING("张三", user->name);
    TEST_ASSERT_EQUAL_STRING("zhangsan@example.com", user->email);
    TEST_ASSERT_TRUE(user->is_active);
    
    user_destroy(user);
}

void test_user_create_invalid_email(void) {
    User* user = NULL;
    UserResult result = user_create(&user, "张三", "invalid-email");
    
    TEST_ASSERT_EQUAL(USER_INVALID_EMAIL, result);
    TEST_ASSERT_NULL(user);
}

void test_user_change_email_success(void) {
    User* user = NULL;
    user_create(&user, "张三", "zhangsan@example.com");
    
    UserResult result = user_change_email(user, "new@example.com");
    
    TEST_ASSERT_EQUAL(USER_SUCCESS, result);
    TEST_ASSERT_EQUAL_STRING("new@example.com", user->email);
    
    user_destroy(user);
}

void test_user_change_email_invalid_format(void) {
    User* user = NULL;
    user_create(&user, "张三", "zhangsan@example.com");
    
    UserResult result = user_change_email(user, "invalid-email");
    
    TEST_ASSERT_EQUAL(USER_INVALID_EMAIL, result);
    TEST_ASSERT_EQUAL_STRING("zhangsan@example.com", user->email); // 邮箱不应该改变
    
    user_destroy(user);
}

int main(void) {
    UNITY_BEGIN();
    
    RUN_TEST(test_user_create_success);
    RUN_TEST(test_user_create_invalid_email);
    RUN_TEST(test_user_change_email_success);
    RUN_TEST(test_user_change_email_invalid_format);
    
    return UNITY_END();
}
```

### 内存管理最佳实践

#### 资源管理模式
```c
// resource_manager.h - 资源管理器
#ifndef RESOURCE_MANAGER_H
#define RESOURCE_MANAGER_H

#include <stddef.h>

typedef struct {
    void* data;
    size_t size;
    void (*cleanup)(void* data);
} Resource;

typedef struct {
    Resource* resources;
    size_t count;
    size_t capacity;
} ResourceManager;

ResourceManager* resource_manager_create(void);
void resource_manager_add(ResourceManager* manager, void* data, size_t size, void (*cleanup)(void*));
void resource_manager_cleanup_all(ResourceManager* manager);
void resource_manager_destroy(ResourceManager* manager);

// RAII 风格的宏
#define RESOURCE_GUARD(manager, ptr, size, cleanup) \
    do { \
        resource_manager_add(manager, ptr, size, cleanup); \
    } while(0)

#endif // RESOURCE_MANAGER_H
```

#### 安全的字符串处理
```c
// safe_string.h - 安全字符串操作
#ifndef SAFE_STRING_H
#define SAFE_STRING_H

#include <stddef.h>
#include <stdbool.h>

typedef enum {
    STR_SUCCESS,
    STR_BUFFER_TOO_SMALL,
    STR_INVALID_INPUT,
    STR_MEMORY_ERROR
} StringResult;

StringResult safe_strcpy(char* dest, size_t dest_size, const char* src);
StringResult safe_strcat(char* dest, size_t dest_size, const char* src);
StringResult safe_snprintf(char* dest, size_t dest_size, const char* format, ...);
bool safe_strcmp(const char* str1, const char* str2);
size_t safe_strlen(const char* str, size_t max_len);

#endif // SAFE_STRING_H
```

### 错误处理和日志系统

#### 统一错误处理
```c
// error_handler.h - 错误处理系统
#ifndef ERROR_HANDLER_H
#define ERROR_HANDLER_H

#include <stdio.h>

typedef enum {
    LOG_DEBUG,
    LOG_INFO,
    LOG_WARNING,
    LOG_ERROR,
    LOG_FATAL
} LogLevel;

typedef enum {
    ERR_SUCCESS = 0,
    ERR_INVALID_PARAMETER = -1,
    ERR_MEMORY_ALLOCATION = -2,
    ERR_FILE_NOT_FOUND = -3,
    ERR_PERMISSION_DENIED = -4,
    ERR_NETWORK_ERROR = -5,
    ERR_TIMEOUT = -6,
    ERR_UNKNOWN = -100
} ErrorCode;

void log_message(LogLevel level, const char* file, int line, const char* format, ...);
const char* error_to_string(ErrorCode error);

#define LOG_DEBUG(format, ...) log_message(LOG_DEBUG, __FILE__, __LINE__, format, ##__VA_ARGS__)
#define LOG_INFO(format, ...) log_message(LOG_INFO, __FILE__, __LINE__, format, ##__VA_ARGS__)
#define LOG_WARNING(format, ...) log_message(LOG_WARNING, __FILE__, __LINE__, format, ##__VA_ARGS__)
#define LOG_ERROR(format, ...) log_message(LOG_ERROR, __FILE__, __LINE__, format, ##__VA_ARGS__)
#define LOG_FATAL(format, ...) log_message(LOG_FATAL, __FILE__, __LINE__, format, ##__VA_ARGS__)

#endif // ERROR_HANDLER_H
```

### 性能优化指南

#### 内存池实现
```c
// memory_pool.h - 内存池
#ifndef MEMORY_POOL_H
#define MEMORY_POOL_H

#include <stddef.h>
#include <stdbool.h>

typedef struct MemoryPool MemoryPool;

MemoryPool* memory_pool_create(size_t block_size, size_t block_count);
void* memory_pool_alloc(MemoryPool* pool);
void memory_pool_free(MemoryPool* pool, void* ptr);
void memory_pool_destroy(MemoryPool* pool);
bool memory_pool_is_full(MemoryPool* pool);
size_t memory_pool_available_blocks(MemoryPool* pool);

#endif // MEMORY_POOL_H
```

## 开发强制要求 ⚠️

1. **内存管理强制要求：** 每个 malloc 必须有对应的 free，使用 Valgrind 验证
2. **边界检查强制要求：** 所有数组访问和字符串操作都要进行边界检查
3. **返回值检查强制要求：** 所有函数返回值都必须检查，特别是内存分配
4. **指针安全要求：** 指针使用后立即置为 NULL，避免野指针
5. **编译警告零容忍：** 必须使用 -Wall -Wextra 编译选项且无警告
6. **标准遵循：** 严格遵循 C99 或 C11 标准，避免编译器扩展
7. **测试覆盖率要求：** 核心模块测试覆盖率不低于 90%
8. **静态分析要求：** 代码必须通过 Clang Static Analyzer 和 Cppcheck 检查

## 构建系统配置

### Makefile 示例
```makefile
CC = gcc
CFLAGS = -std=c11 -Wall -Wextra -Werror -g -O2
LDFLAGS = 
SRCDIR = src
INCDIR = include
TESTDIR = tests
OBJDIR = build

# 源文件
SOURCES = $(wildcard $(SRCDIR)/**/*.c $(SRCDIR)/*.c)
OBJECTS = $(SOURCES:$(SRCDIR)/%.c=$(OBJDIR)/%.o)

# 测试文件
TEST_SOURCES = $(wildcard $(TESTDIR)/**/*.c $(TESTDIR)/*.c)
TEST_OBJECTS = $(TEST_SOURCES:$(TESTDIR)/%.c=$(OBJDIR)/test_%.o)

# 目标
TARGET = program
TEST_TARGET = test_program

.PHONY: all clean test install

all: $(TARGET)

$(TARGET): $(OBJECTS)
	$(CC) $(OBJECTS) -o $@ $(LDFLAGS)

$(OBJDIR)/%.o: $(SRCDIR)/%.c
	@mkdir -p $(dir $@)
	$(CC) $(CFLAGS) -I$(INCDIR) -c $< -o $@

test: $(TEST_TARGET)
	./$(TEST_TARGET)

$(TEST_TARGET): $(TEST_OBJECTS) $(filter-out $(OBJDIR)/main.o, $(OBJECTS))
	$(CC) $^ -o $@ $(LDFLAGS)

$(OBJDIR)/test_%.o: $(TESTDIR)/%.c
	@mkdir -p $(dir $@)
	$(CC) $(CFLAGS) -I$(INCDIR) -I$(TESTDIR) -c $< -o $@

clean:
	rm -rf $(OBJDIR) $(TARGET) $(TEST_TARGET)

install: $(TARGET)
	cp $(TARGET) /usr/local/bin/

# 静态分析
analyze:
	clang-static-analyzer $(SOURCES)
	cppcheck --enable=all $(SRCDIR)

# 内存检查
memcheck: $(TARGET)
	valgrind --leak-check=full --show-leak-kinds=all ./$(TARGET)
```

### CMakeLists.txt 示例
```cmake
cmake_minimum_required(VERSION 3.10)
project(MyProject C)

set(CMAKE_C_STANDARD 11)
set(CMAKE_C_STANDARD_REQUIRED ON)

# 编译选项
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wall -Wextra -Werror")
set(CMAKE_C_FLAGS_DEBUG "-g -O0")
set(CMAKE_C_FLAGS_RELEASE "-O2 -DNDEBUG")

# 包含目录
include_directories(include)

# 源文件
file(GLOB_RECURSE SOURCES "src/*.c")
file(GLOB_RECURSE TEST_SOURCES "tests/*.c")

# 主程序
add_executable(${PROJECT_NAME} ${SOURCES})

# 测试程序
enable_testing()
add_executable(test_${PROJECT_NAME} ${TEST_SOURCES} ${SOURCES})
add_test(NAME UnitTests COMMAND test_${PROJECT_NAME})

# 安装
install(TARGETS ${PROJECT_NAME} DESTINATION bin)

# 文档生成
find_package(Doxygen)
if(DOXYGEN_FOUND)
    configure_file(${CMAKE_CURRENT_SOURCE_DIR}/Doxyfile.in ${CMAKE_CURRENT_BINARY_DIR}/Doxyfile @ONLY)
    add_custom_target(doc
        ${DOXYGEN_EXECUTABLE} ${CMAKE_CURRENT_BINARY_DIR}/Doxyfile
        WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}
        COMMENT "Generating API documentation with Doxygen"
        VERBATIM
    )
endif()
```

## 注意事项

- 时刻关注内存安全，避免缓冲区溢出和内存泄漏
- 使用静态分析工具及时发现潜在问题
- 编写防御性代码，对所有输入进行验证
- 注意代码的可移植性，避免使用平台特定的特性
- 合理使用宏定义，但避免过度使用
- 重视代码的可读性和维护性
- 定期使用 Valgrind 等工具检查内存问题
- 遵循 MISRA C 标准（如果适用）

这个规范强调了 C 语言的安全性、性能和可维护性，同时适配了 DDD + TDD 的开发理念，为系统级编程提供了全面的指导。