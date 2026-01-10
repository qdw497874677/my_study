# AI Coding Agent Guide

> 本文档用于指导 AI Coding Agent (如 Sisyphus/Cursor/Cline/OpenCode) 在本代码库中工作。
> 目标：提供清晰的上下文、工具使用方式、代码规范和最佳实践。

---

## 📋 目录

- [项目概览](#项目概览)
- [代码库结构](#代码库结构)
- [项目类型](#项目类型)
- [技术栈](#技术栈)
- [开发规范](#开发规范)
- [构建、测试和 lint 命令](#构建测试和-lint-命令)
- [工作流和最佳实践](#工作流和最佳实践)

---

## 项目概览

### 项目名称
**AI Coding 内部分享研究项目**

### 项目目的
- 研究 AI Coding 工具和最佳实践
- 准备公司内部分享材料
- 整理开发范式和 Subagent 使用经验

### 项目特点
- **研究为主**：非生产代码库，专注于文档和案例研究
- **文档驱动**：Markdown 格式，易于维护和分享
- **持续迭代**：根据 AI Coding 发展不断更新

---

## 代码库结构

```
ai-coding-sharing-outline.md/          # 主大纲文档
AGENTS.md/                           # Agent 指南（本文件）
```

### 目录说明

- **ai-coding-sharing-outline.md**：主文档，包含完整的分享大纲
  - 背景与动机
  - 主流工具介绍
  - 开发范式变化（包括 Subagent 系统）
  - 最佳实践
  - 实战案例
  - 常见误区与风险
  - 行动建议

- **AGENTS.md**：本文件，用于指导 AI Agent 工作
  - 代码库上下文
  - 工具使用方式
  - 代码规范
  - 命令参考
  - 最佳实践

---

## 项目类型

### 研究项目
本仓库是一个**研究型项目**，而非生产代码库。

**对 Agent 的影响**：
- ✅ **文档优先**：Agent 应优先阅读本文档了解项目背景
- ✅ **无编译要求**：无需关注构建、类型检查等
- ✅ **迭代友好**：文档内容会持续更新，Agent 需要关注最新版本

### 文档体系
- **ai-coding-sharing-outline.md**：核心大纲，约 1000+ 行
  - 包含完整分享框架
  - 已更新 Subagent 相关内容
- **AGENTS.md**：Agent 指南
  - 本文件
  - 约 150 行目标
  - 提供可操作的指导

---

## 技术栈

### 文档格式
- **Markdown**：所有文档使用 Markdown 格式
- **结构化**：使用标题层级、列表、代码块

### 工具生态
- **主要工具**：Claude Code, Cursor, OpenCode, Copilot, Cline
- **Subagent 系统**：explore, librarian, oracle, specialist agents
- **Spec Driven**：Speckit, OpenSpec

---

## 开发规范

### 命名约定

#### 文件命名
- 使用 **kebab-case**（小写，短横线分隔）
- 示例：`user-service.ts`, `auth-helper.ts`, `build-and-test.sh`

#### 目录命名
- 使用 **kebab-case**
- 示例：`components/`, `utils/`, `api/`, `tests/`

#### 组件命名
- React: **PascalCase**（首字母大写）
  - 示例：`UserProfile`, `AuthService`, `DataGrid`
- TypeScript/Type: **PascalCase**
  - 示例：`UserService`, `AuthService`, `ConfigManager`
- Python: **PascalCase** 或 **snake_case**
  - 示例：`UserProfile`, `user_profile`, `ConfigManager`

#### 变量命名
- JavaScript/TypeScript/Python: **camelCase**（首字母小写，驼峰）
  - 示例：`userName`, `accessToken`, `isLoggedIn`
- 常量：**UPPER_SNAKE_CASE**（全大写，下划线）
  - 示例：`MAX_RETRY_COUNT`, `API_BASE_URL`, `DB_HOST`

#### 函数命名
- **动词开头**，驼峰
- 示例：`getUserById()`, `fetchUserData()`, `calculateHash()`
- ✅ **推荐**：使用动词（get, fetch, calculate, create, update, delete）
- ❌ **避免**：使用名词（user, data, info）

### 导入规范

#### 按类型
```typescript
// 推荐优先级
import { Component } from '@/components/common/Button';
import { UserService } from '@/services/user/UserService';
import { APIConfig } from '@/config/api';

// 库导入放在前面，第三方导入放在后面
import { useState, useEffect } from 'react';
import axios from 'axios';
import { z } from 'zod';
```

```python
# 推荐优先级
from typing import List, Dict, Optional
import requests
from dataclasses import dataclass

# 标准库在前，第三方库在后
import pandas as pd
import numpy as np
from requests import get
```

#### 别名（避免）
```typescript
// ❌ 不推荐
import { Button as Btn } from '@/components/Button';
import { UserService as US } from '@/services/UserService';
import { APIClient as API } from '@/utils/api';

// ✅ 推荐：使用全名，提高可读性
import { Button } from '@/components/common/Button';
import { UserService } from '@/services/user/UserService';
import { APIClient } from '@/utils/api';
```

### 代码格式

#### 缩进（2 空格）
- ✅ **缩进**：使用 2 空格缩进
- ✅ **尾随大括号**：`{` 后换行
- ✅ **尾随逗号**：`,` 后换行

```typescript
// ✅ 推荐
function calculateTotal(items: Item[]): number {
  let total = 0;
  for (const item of items) {
    total += item.price;
  }
  return total;
}

// ❌ 避免
function calculateTotal(items:Item[]){
    let total=0;
    for(const item of items){
        total+=item.price;
    }
    return total;
}
```

#### 行宽（100-120 字符）
- **推荐**：每行不超过 100 字符（含缩进）
- **工具**：配置 EditorConfig 或使用 Prettier 自动格式化

```typescript
// ✅ 推荐
const API_BASE_URL = process.env.API_BASE_URL || 'https://api.example.com';

interface User {
  id: string;
  name: string;
  email: string;
}

// ❌ 避免
const apiUrl=process.env.API_BASE_URL||'https://api.example.com';

interface User{id:string,name:string,email:string}
```

#### 引号使用
- **字符串**：优先使用单引号 `'`
- **模板字符串**：使用反引号 `` ` `
- **对象属性**：优先使用单引号

```typescript
// ✅ 推荐
const userMessage = `Hello, ${userName}!`;
const config = {
  host: 'localhost',
  port: 3000,
};

// ❌ 避免
const userMessage = "Hello, " + userName + "!";
const config={host:"localhost",port:3000};
```

### 类型安全

#### 避免使用 any
- ❌ **禁止**：`const data: any;`
- ❌ **禁止**：`function processData(input: any): void;`
- ✅ **推荐**：明确定义接口或类型

```typescript
// ❌ 避免
function processUser(data: any): void {
  console.log(data.name);
}

// ✅ 推荐
interface UserData {
  name: string;
  email: string;
}

function processUser(data: UserData): void {
  console.log(data.name);
}
```

#### 使用 Readonly 和 Optional
```typescript
interface User {
  id: string;
  name: string;
  email?: string;  // Optional 属性
}

function updateUser(id: string, updates: Partial<User>): User {
  // ...
}
```

#### 避免 as 断言
- ❌ **禁止**：`data as User;`
- ✅ **推荐**：类型守卫或可选链

```typescript
// ❌ 避免
const user = data as User;

// ✅ 推荐
if (typeof data === 'object' && data !== null && 'name' in data) {
  const user = data as User;
}
```

### 注释规范

#### JSDoc 风格
```typescript
/**
 * Calculate the total price of all items
 *
 * @param items - Array of items with price property
 * @returns Total price as a number
 *
 * @example
 * calculateTotal([{ price: 10 }, { price: 20 }]); // Returns 30
 */
function calculateTotal(items: Item[]): number {
  let total = 0;
  for (const item of items) {
    total += item.price;
  }
  return total;
}
```

#### 注释语言
- ✅ **使用中文**：本仓库文档应使用中文注释
- ✅ **注释与代码同步**：代码变更时同步更新注释

```typescript
// ✅ 推荐
/**
 * 认证服务类
 * 处理用户登录、登出、token 刷新
 */
class AuthService {
  // ...
}

// ❌ 避免
class AuthService {
  // Auth service class for handling login and logout
}
```

### 错误处理

#### 统一错误处理
```typescript
// ✅ 推荐：创建统一的错误处理类
class AppError extends Error {
  constructor(
    public code: string,
    public message: string,
    public statusCode?: number
  ) {
    super(message);
    this.name = 'AppError';
    this.code = code;
    this.statusCode = statusCode;
  }
}

// 使用示例
try {
  await fetchUserData();
} catch (error) {
  throw new AppError('FETCH_FAILED', 'Failed to fetch user data', 500);
}
```

#### 错误码定义
```typescript
enum ErrorCode {
  INVALID_INPUT = 'INVALID_INPUT',
  UNAUTHORIZED = 'UNAUTHORIZED',
  NOT_FOUND = 'NOT_FOUND',
  INTERNAL_ERROR = 'INTERNAL_ERROR',
}

class AppError extends Error {
  constructor(
    public code: ErrorCode,
    message: string,
    statusCode?: number
  ) {
    super(message);
    this.code = code;
  this.statusCode = statusCode;
  }
}
```

#### 日志规范
```typescript
// ✅ 推荐：使用结构化日志
const logger = {
  info: (message: string) => console.log(`[INFO] ${message}`),
  warn: (message: string) => console.warn(`[WARN] ${message}`),
  error: (message: string) => console.error(`[ERROR] ${message}`),
};

// 使用示例
logger.info('User logged in successfully');
logger.error('Failed to fetch data', error);
```

---

## 构建、测试和 lint 命令

### 构建命令

#### 本项目是研究项目
**重要提示**：本仓库**不是需要构建的代码项目**。

**对 Agent 的影响**：
- ❌ **不要尝试运行**：`npm run build`, `npm run dev` 等命令
- ✅ **仅阅读文档**：Agent 应专注于阅读和参考文档内容
- ✅ **使用示例代码**：如需演示，应使用 Markdown 示例而非实际构建

### 如果需要构建（针对未来代码项目）

#### 前端项目（React/TypeScript）
```bash
# 安装依赖
npm install

# 开发服务器
npm run dev

# 构建
npm run build

# 运行测试
npm test

# Lint 检查
npm run lint

# 格式化代码
npm run format
```

#### 后端项目（Node.js）
```bash
# 安装依赖
npm install

# 开发模式（自动重启）
npm run dev

# 构建
npm run build

# 运行测试
npm test

# Lint
npm run lint
```

### 测试命令

#### 单元测试（Unit Tests）
```bash
# 运行所有测试
npm test

# 运行特定测试文件
npm test -- auth.test.ts

# 运行带覆盖率的测试
npm test -- --coverage

# 监听模式（开发时自动运行）
npm run test:watch
```

#### 集成测试（Integration Tests）
```bash
# 运行集成测试
npm run test:integration

# 运行端到端测试
npm run test:e2e
```

### Lint 命令

#### ESLint
```bash
# 运行 ESLint 检查
npm run lint

# 自动修复问题
npm run lint:fix

# 检查特定文件
npm run lint src/auth/

# 使用缓存
npm run lint --cache
```

#### Prettier
```bash
# 检查代码格式
npm run format:check

# 自动格式化
npm run format

# 格式化特定文件
npm run format:write src/
```

#### TypeScript 类型检查
```bash
# 类型检查
npm run type-check

# 监听模式
npm run type-check:watch
```

---

## 工作流和最佳实践

### Agent 工作流程

#### 第一阶段：理解项目（Ask 模式）
```
优先阅读以下文档：
1. ai-coding-sharing-outline.md - 了解分享大纲
2. AGENTS.md - 本文档 - 了解代码规范

当需要实现功能时：
1. 明确任务范围
2. 选择合适的 Agent 类型（explore/librarian/oracle/specialist）
3. 提供充分的上下文和约束
```

#### 第二阶段：设计方案（Plan 模式）
```
使用以下工具协作：
- @librarian 查找相关文档和最佳实践
- @oracle 获取架构建议

输出要求：
1. 技术方案（包括技术栈选择）
2. 架构设计（模块划分、接口设计）
3. 实现计划（任务拆解、优先级）
```

#### 第三阶段：实现功能（Agent 模式）
```
实现时遵循规范：
1. 命名规范（PascalCase, camelCase）
2. 类型安全（避免 any，使用明确定义）
3. 错误处理（统一的 Error 类和错误码）
4. 代码格式（2 空格缩进，100 字符行宽）
5. 注释规范（JSDoc，中文注释）
```

#### 第四阶段：测试验证
```
测试要求：
1. 单元测试覆盖率 > 80%
2. 所有测试通过后才能合并
3. Lint 检查无错误
4. 代码格式化通过 Prettier
```

### 使用 Subagent 的最佳实践

#### 任务拆分
```
原则：将复杂任务拆分为 1-2 小时可完成的子任务

示例：
❌ 错误做法：
"实现一个完整的用户管理系统（包括认证、权限、CRUD）"

✅ 正确做法：
"第一阶段：实现用户认证功能（登录、登出、token 刷新）"
"第二阶段：实现用户权限检查功能"
"第三阶段：实现用户 CRUD 功能"
```

#### 并行执行
```
当有多个独立任务时，使用 parallel 或 background_task：

示例：
# 同时启动多个 subagent
background_task(agent="explore", prompt="Find all authentication related files")
background_task(agent="explore", prompt="Search for authorization patterns")

# 收敛结果后综合决策
```

#### 上下文管理
```
提供关键上下文：
1. 项目技术栈（React + TypeScript + Node.js）
2. 相关文档链接
3. 代码示例（如果参考现有实现）
4. 明确的约束条件（性能要求、兼容性）
```

### 提示词（Prompt）模板

#### 设计阶段
```markdown
## 设计一个用户管理 API

### 技术栈
- 前端：React + TypeScript
- 后端：Node.js + Express
- 数据库：PostgreSQL
- 认证：JWT + Bcrypt

### 核心功能
1. 用户注册（用户名、邮箱、密码）
2. 用户登录（生成 JWT token）
3. 用户信息获取
4. 用户信息更新
5. 用户删除

### 设计要求
1. 所有 API 必须包含错误处理
2. 使用标准 HTTP 状态码
3. 密码必须使用 bcrypt 加密（salt: 10）
4. Token 有效期为 24 小时
5. 遵循 RESTful 规范

### 约束
- 禁止使用 SQL 注入（使用参数化查询）
- 禁止硬编码密钥（从环境变量读取）
- 所有公共 API 必须进行认证
```

#### 实现阶段
```markdown
## 实现 Auth API

### 后端实现

#### 用户注册
```typescript
// src/services/auth/register.ts
import bcrypt from 'bcrypt';
import { prisma } from '@/lib/prisma';
import { AppError, ErrorCode } from '@/utils/errors';

interface RegisterInput {
  username: string;
  email: string;
  password: string;
}

export async function register(input: RegisterInput): Promise<void> {
  // 1. 验证输入
  if (!input.username || !input.email || !input.password) {
    throw new AppError(ErrorCode.INVALID_INPUT, 'All fields are required');
  }

  // 2. 检查用户是否存在
  const existingUser = await prisma.user.findUnique({
    where: { OR: [{ username: input.username }, { email: input.email }]
  });

  if (existingUser) {
    throw new AppError(ErrorCode.INVALID_INPUT, 'Username or email already exists');
  }

  // 3. 加密密码
  const hashedPassword = await bcrypt.hash(input.password, 10);

  // 4. 创建用户
  await prisma.user.create({
    data: {
      username: input.username,
      email: input.email,
      password: hashedPassword,
    }
  });

  // 5. 返回成功
  return;
}
```

#### 用户登录
```typescript
// src/services/auth/login.ts
import jwt from 'jsonwebtoken';
import bcrypt from 'bcrypt';
import { prisma } from '@/lib/prisma';
import { AppError, ErrorCode } from '@/utils/errors';
import { config } from '@/config';

export async function login(username: string, password: string): Promise<string> {
  // 1. 查找用户
  const user = await prisma.user.findUnique({
    where: { username }
  });

  if (!user) {
    throw new AppError(ErrorCode.UNAUTHORIZED, 'Invalid username or password');
  }

  // 2. 验证密码
  const isValidPassword = await bcrypt.compare(password, user.password);

  if (!isValidPassword) {
    throw new AppError(ErrorCode.UNAUTHORIZED, 'Invalid username or password');
  }

  // 3. 生成 JWT token
  const token = jwt.sign(
    { userId: user.id, username: user.username },
    config.jwtSecret,
    { expiresIn: '24h' }
  );

  return token;
}
```

### 测试要求
```typescript
// src/__tests__/auth.test.ts
import { register } from '@/services/auth/register';
import { login } from '@/services/auth/login';

describe('Authentication Service', () => {
  describe('Register', () => {
    it('should register a new user successfully', async () => {
      const result = await register({
        username: 'testuser',
        email: 'test@example.com',
        password: 'password123',
      });
      expect(result).not.toThrow();
    });

    it('should throw error if username already exists', async () => {
      await expect(register({
        username: 'existinguser',
        email: 'existing@example.com',
        password: 'password123',
      })).rejects.toThrow();
    });
  });

  describe('Login', () => {
    it('should return token for valid credentials', async () => {
      const token = await login('testuser', 'password123');
      expect(typeof token).toBe('string');
      expect(token.length).toBeGreaterThan(0);
    });

    it('should throw error for invalid credentials', async () => {
      await expect(login('testuser', 'wrongpassword')).rejects.toThrow();
    });
  });
});
```

```

#### 验收标准
```
✅ 必须满足：
1. 所有测试通过
2. Lint 检查无错误
3. 代码覆盖率 > 80%
4. 遵循命名规范
5. 包含必要的注释

❌ 不符合要求：
1. 测试失败
2. 存在类型错误
3. Lint 错误
4. 代码格式不规范
```

### 常见任务

#### 任务类型和推荐工具
| 任务类型 | 推荐工具 | 理由 |
|---------|---------|------|
| **快速查询** | `grep` / `rg` | 简单字符串搜索 |
| **复杂搜索** | `ast_grep` / `ast-grep-replace` | AST 模式匹配 |
| **文件操作** | `read` / `write` / `edit` | 直接文件读写 |
| **符号查找** | `lsp_workspace_symbols` / `lsp_goto_definition` | LSP 导航 |
| **批量操作** | `bash` | Shell 命令执行 |
| **类型检查** | `lsp_diagnostics` | 类型诊断 |

#### 工作模式
```
探索阶段（1-2 分钟）：
- 使用 @explore 快速了解代码库结构
- 使用 @librarian 查找相关文档

设计阶段（5-10 分钟）：
- 使用 @oracle 获取架构建议
- 明确技术方案和约束

实现阶段（根据任务复杂度）：
- 简单任务：直接在主对话完成
- 复杂任务：考虑拆分为多个子任务
- 大型任务：创建新的对话分支

验证阶段：
- 运行测试确保功能正确
- 使用 @code-reviewer 检查代码质量
- 使用 Lint 确保代码规范
```

---

## 附录

### 常用命令速查表

| 命令 | 用途 |
|------|------|
| `ls -la` | 列出文件和目录详情 |
| `grep -r "pattern"` | 递归搜索文件内容 |
| `find . -name "*.ts"` | 查找特定类型文件 |
| `head -n 20 file.txt` | 查看文件前 20 行 |
| `tail -f log.txt` | 实时查看日志文件 |
| `wc -l file.txt` | 统计文件行数、字数 |

### 常见错误和解决方案

| 错误 | 解决方案 |
|------|---------|
| "Module not found" | 检查导入路径，使用相对导入 |
| "Cannot find module" | 安装缺失的依赖 `npm install` |
| "Type error: cannot find name" | 检查类型定义，确保正确导入 |
| "Lint errors" | 运行 `npm run lint:fix` 自动修复 |

---

## 注意事项

### Agent 协作时
- ✅ **并行使用多个 subagent** 提高效率
- ✅ **及时收敛结果** 避免任务无限期
- ✅ **明确输出要求** 减少返工

### 代码质量
- ✅ **类型安全优先** 避免 any 类型
- ✅ **错误处理完善** 统一错误码和异常处理
- ✅ **注释和文档同步** 代码变更时更新相关文档
- ✅ **测试覆盖率** 单元测试覆盖率 > 80%

### 项目特性
- 📚 **研究导向**：专注于文档和案例整理
- 🔄 **持续迭代**：根据 AI Coding 发展更新内容
- 🤖 **Agent 友好**：提供充分的上下文和指导

---

**最后更新**：2025-01-09
