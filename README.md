# syntax-highlight-sample

本文件用于验收 Markdown 渲染中各语言代码块的语法高亮效果，目标是与 GitHub 渲染保持一致。

每个代码块都尽量覆盖了该语言的常见语法元素：关键字、字符串、数字、注释、操作符、内置函数、装饰器/属性等，方便快速对比着色差异。

---

## 1. JavaScript

```javascript
// 用户管理模块 —— 演示 ES6+ 常见语法
import { createHash } from 'node:crypto';

const API_BASE = 'https://api.example.com/v1';
const MAX_RETRY = 3;

/**
 * 用户类
 * @param {string} name - 用户昵称
 */
class User {
  #password; // 私有字段

  constructor(name, age = 18) {
    this.name = name;
    this.age = age;
    this.tags = new Set(['default']);
  }

  static fromJSON(json) {
    return new User(json.name, json.age);
  }

  async fetchProfile() {
    try {
      const res = await fetch(`${API_BASE}/users/${this.name}`);
      if (!res.ok) throw new Error(`HTTP ${res.status}`);
      return await res.json();
    } catch (err) {
      console.error('Fetch failed:', err);
      return null;
    }
  }
}

// 模板字符串、解构、扩展运算符
const users = [new User('Alice'), new User('Bob', 25)];
const [first, ...rest] = users;
const summary = users.map(u => ({ ...u, hash: createHash('sha256') }));

// 正则表达式 & 三元
const isEmail = /^[\w.+-]+@[\w-]+\.[\w.-]+$/;
const valid = isEmail.test('hi@example.com') ? 'yes' : 'no';

export default User;
```

---

## 2. HTML

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>语法高亮示例</title>
  <link rel="stylesheet" href="/styles/main.css" />
  <style>
    body { font-family: -apple-system, sans-serif; }
  </style>
</head>
<body>
  <!-- 顶部导航 -->
  <header class="navbar" id="top">
    <a href="#home" data-route="home">首页</a>
    <a href="#about" data-route="about">关于</a>
  </header>

  <main>
    <h1>Hello, <em>World</em>!</h1>
    <p>这是一段 <strong>加粗</strong> 文字，含有 &amp; 转义字符。</p>

    <form action="/submit" method="POST">
      <label for="email">邮箱：</label>
      <input type="email" id="email" name="email" required placeholder="you@example.com" />
      <button type="submit" disabled>提交</button>
    </form>

    <img src="./logo.svg" alt="Logo" width="120" />
  </main>

  <script src="/app.js" defer></script>
</body>
</html>
```

---

## 3. CSS

```css
/* 全局变量 */
:root {
  --primary: #07c160;
  --text: #1f1f1f;
  --radius: 8px;
}

* {
  box-sizing: border-box;
  margin: 0;
}

body {
  font-family: 'PingFang SC', -apple-system, sans-serif;
  color: var(--text);
  background: linear-gradient(135deg, #fafafa 0%, #f0f0f0 100%);
}

.button {
  display: inline-flex;
  align-items: center;
  padding: 8px 16px;
  border-radius: var(--radius);
  background-color: var(--primary);
  color: #fff;
  transition: opacity 0.2s ease-in-out;
}

.button:hover,
.button:focus-visible {
  opacity: 0.85;
  cursor: pointer;
}

.button[disabled] {
  opacity: 0.4 !important;
  pointer-events: none;
}

/* 媒体查询 & 嵌套伪类 */
@media (max-width: 768px) {
  .navbar > a:not(:last-child)::after {
    content: '|';
    margin: 0 8px;
  }
}

@keyframes fadeIn {
  from { opacity: 0; transform: translateY(10px); }
  to   { opacity: 1; transform: translateY(0); }
}
```

---

## 4. JSON

```json
{
  "name": "syntax-highlight-sample",
  "version": "1.0.0",
  "private": true,
  "description": "用于验收 Markdown 语法高亮效果的样本",
  "keywords": ["markdown", "highlight", "github"],
  "author": {
    "name": "Boren",
    "email": "boren@example.com"
  },
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "test": "vitest run"
  },
  "dependencies": {
    "react": "^18.2.0",
    "lodash": "~4.17.21"
  },
  "config": {
    "port": 3000,
    "https": false,
    "fallback": null,
    "tags": ["beta", "internal"],
    "limits": {
      "maxFileSize": 10485760,
      "rateLimit": 0.5
    }
  }
}
```

---

## 5. Python

```python
"""用户数据处理模块 —— 演示 Python 常见语法"""
from __future__ import annotations

import asyncio
from dataclasses import dataclass, field
from typing import Optional

API_BASE = "https://api.example.com/v1"
MAX_RETRY: int = 3


@dataclass
class User:
    """用户数据类"""
    name: str
    age: int = 18
    tags: list[str] = field(default_factory=lambda: ["default"])

    def __post_init__(self) -> None:
        if self.age < 0:
            raise ValueError(f"年龄不能为负数: {self.age}")

    @classmethod
    def from_dict(cls, data: dict) -> "User":
        return cls(name=data["name"], age=data.get("age", 18))

    @property
    def is_adult(self) -> bool:
        return self.age >= 18


async def fetch_profile(user: User) -> Optional[dict]:
    """异步获取用户信息"""
    for attempt in range(1, MAX_RETRY + 1):
        try:
            # 模拟网络请求
            await asyncio.sleep(0.1)
            return {"name": user.name, "score": 99.5}
        except (TimeoutError, ConnectionError) as e:
            print(f"[{attempt}/{MAX_RETRY}] 请求失败: {e!r}")
    return None


def main() -> None:
    users = [User("Alice"), User("Bob", age=25)]
    adults = [u for u in users if u.is_adult]

    # 字典推导式 + f-string
    scores = {u.name: u.age * 1.5 for u in adults}
    print(f"成年用户分数: {scores}")

    # 解包 & 三元
    first, *rest = users
    label = "single" if not rest else "multiple"
    print(rf"标签: {label}\n首位: {first.name}")


if __name__ == "__main__":
    main()
```

---

## 6. Bash

```bash
#!/usr/bin/env bash
# 部署脚本 —— 演示 Bash 常见语法
set -euo pipefail

# 变量与默认值
readonly APP_NAME="my-app"
readonly DEPLOY_DIR="${DEPLOY_DIR:-/var/www/${APP_NAME}}"
VERSION="${1:-latest}"

# 函数定义
log() {
  local level="$1"; shift
  echo "[$(date +'%Y-%m-%d %H:%M:%S')] [${level}] $*"
}

cleanup() {
  log INFO "清理临时文件..."
  rm -rf /tmp/"${APP_NAME}".*
}
trap cleanup EXIT

# 主流程
log INFO "开始部署 ${APP_NAME} (版本: ${VERSION})"

if [[ ! -d "${DEPLOY_DIR}" ]]; then
  log WARN "目录不存在，创建中: ${DEPLOY_DIR}"
  mkdir -p "${DEPLOY_DIR}"
fi

# 数组与循环
services=("nginx" "redis" "postgres")
for svc in "${services[@]}"; do
  if systemctl is-active --quiet "${svc}"; then
    log OK "服务 ${svc} 运行中 ✓"
  else
    log ERR "服务 ${svc} 未启动!" >&2
    exit 1
  fi
done

# 管道与命令替换
file_count=$(find "${DEPLOY_DIR}" -type f -name "*.log" | wc -l)
log INFO "日志文件数量: ${file_count}"

# Heredoc
cat <<EOF > /etc/myapp.conf
app_name=${APP_NAME}
version=${VERSION}
debug=false
EOF

log INFO "部署完成 🎉"
exit 0
```

---

## 7. YAML

```yaml
# CI/CD 流水线配置
name: Build & Deploy
on:
  push:
    branches: [main, develop]
  pull_request:
    types: [opened, synchronize]

env:
  NODE_VERSION: "20"
  REGISTRY: ghcr.io

jobs:
  build:
    name: 构建任务
    runs-on: ubuntu-latest
    timeout-minutes: 15
    strategy:
      matrix:
        node: [18, 20, 22]
        os: [ubuntu-latest, macos-latest]
      fail-fast: false

    steps:
      - name: Checkout
        uses: actions/checkout@v4
        with:
          fetch-depth: 0

      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: ${{ matrix.node }}
          cache: "npm"

      - name: Install & Build
        run: |
          npm ci
          npm run build
        env:
          CI: true
          API_KEY: ${{ secrets.API_KEY }}

      # 多行字符串
      - name: Print banner
        run: |
          echo "==============="
          echo "Build complete!"
          echo "==============="

  config_demo:
    server:
      host: 0.0.0.0
      port: 8080
      tls: true
    features:
      - auth
      - logging
      - metrics
    limits: { cpu: 2, memory: "512Mi" }
    description: >
      这是一段折叠风格的多行
      字符串，换行会被替换为空格。
    notes: |
      这是一段保留风格的多行
      字符串，换行会被保留。
```

---

## 8. Markdown

````markdown
# 一级标题

## 二级标题

### 三级标题

这是一段普通正文，包含 **加粗**、*斜体*、~~删除线~~ 和 `行内代码`。

> 这是一段引用块。
> 引用块可以跨多行。
>
> > 嵌套的引用块。

## 列表

- 无序列表项 1
- 无序列表项 2
  - 嵌套项 a
  - 嵌套项 b
- 无序列表项 3

1. 有序列表项 1
2. 有序列表项 2
3. 有序列表项 3

- [x] 已完成的任务
- [ ] 待办任务

## 链接与图片

这是一个 [行内链接](https://github.com)，这是一个 [带标题链接](https://github.com "GitHub")。

![图片描述](https://example.com/image.png)

## 表格

| 语言       | 类型     | 难度 |
| ---------- | :------: | ---: |
| JavaScript | 解释型   | 中等 |
| Python     | 解释型   | 简单 |
| Rust       | 编译型   | 困难 |

## 代码

行内代码：`const x = 42;`

代码块：

```js
function hello(name) {
  return `Hello, ${name}!`;
}
```

## 分隔线

---

## 其他

H~2~O 与 X^2^（部分渲染器支持）

脚注示例[^1]

[^1]: 这是脚注内容。
````
