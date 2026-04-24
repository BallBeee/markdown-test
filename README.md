# markdown-test

## P0（Web 与设计工程基石）

### `JavaScript`

前端组件逻辑、交互行为编写。`TypeScript` 的类型注解（Type Annotations）和泛型（Generics）是大部分轻量级解析器的噩梦，极易解析崩溃，必须重点验收。

### `HTML` & `XML`

DOM 结构、各类标记语言。需要重点关注嵌套在标签内的属性（Attributes）和字符串高亮是否清晰分离。

### `CSS` / `SCSS` / `LESS`

样式表。验收重点在于伪类（Pseudo-classes）、CSS 变量（CSS Variables）以及嵌套规则下的层级渲染。

### `JSON`

这一项极其重要。无论是导出 Figma 变量（Variables）、构建 Design Tokens，还是进行 Agentic UI（代理化用户界面）的 API 联调，`JSON` 都是最核心的载体。必须确保键名（Keys）和键值（Values）中的字符串在视觉上有明确的色彩区分，而不能糊成一种颜色。

## P1（AI、脚本与配置）

这类语言常用于自动化流程、AI 模型交互、环境配置以及终端命令。

### `Python`

AI 脚本编写、数据处理、后端逻辑。语法结构依赖缩进，没有大括号，需要检查高亮引擎对函数定义（`def`）、装饰器（`@`）和保留字的区别能力。

### `Bash` / `Shell`

终端命令行（CLI）指令。无论是配置 OpenClaw 这类本地服务的环境，还是日常的 Git 操作，终端代码块都是文档中的常客。重点验收系统命令和参数（如 `v`, `-config`）的高亮。

### `YAML`

CI/CD 管道配置、各类系统配置文件。与 `JSON` 类似，重点在于准确呈现基于缩进的数据层级结构。

### `Markdown`

「用 Markdown 来展示 Markdown 语法」。检查引擎是否能正确高亮 Markdown 自身的语法标记（如加粗、列表、引用）。

```markdown
> ## [Link](# "_Italic_") `<tag>`!
- [x] Task **bold _italic_** & \*\*esc\*\*.
- [ ] [Text \[nest\]][ref] with `` `inline` ``.
***
```code``` is inline text, not a code block.
[ref]: https://url.com/ "Title \"Quote\""
```
