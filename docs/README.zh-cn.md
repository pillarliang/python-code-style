# Python 代码风格插件

🌍 **语言**: [English](../README.md) | [中文简体](README.zh-cn.md) | [繁體中文](README.zh-tw.md) | [Deutsch](README.de.md) | [Français](README.fr.md) | [Italiano](README.it.md) | [日本語](README.ja.md) | [한국어](README.ko.md) | [Português](README.pt.md) | [Español](README.es.md)

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Claude Code Plugin](https://img.shields.io/badge/Claude%20Code-Plugin-blue.svg)](https://code.claude.com/docs/en/plugins)

一个 Claude Code 插件，用于在生成 Python 代码时强制执行专业的代码风格规范。

## 功能特性

- **自动激活**：Claude 在生成或审查代码时自动遵循 Python 风格指南
- **代码审查支持**：审查现有 Python 代码，提供详细反馈和评分
- **全面覆盖**：包含行业标准最佳实践
  - 命名规范（模块、类、函数、变量、常量）
  - 文档字符串格式（Args、Returns、Raises、Yields 部分）
  - 导入规则和排序
  - 格式化标准（缩进、行长度、空白）
  - 语言规则（异常、类型提示、推导式）
- **详细参考**：边缘情况的支持文档

## 安装

### 方法 1：通过 Marketplace（推荐）

在 Claude Code 中运行：

```bash
# 步骤 1：添加 marketplace
/plugin marketplace add pillarliang/python-code-style

# 步骤 2：安装插件
/plugin install python-code-style
```

### 方法 2：通过 settings.json

添加到 `~/.claude/settings.json`：

```json
{
  "extraKnownMarketplaces": {
    "python-code-style": {
      "source": {
        "source": "github",
        "repo": "pillarliang/python-code-style"
      }
    }
  },
  "enabledPlugins": {
    "python-code-style@python-code-style": true
  }
}
```

### 方法 3：手动安装

```bash
# 克隆仓库
git clone https://github.com/pillarliang/python-code-style.git

# 复制到 Claude 插件目录
cp -r python-code-style ~/.claude/plugins/python-code-style
```

### 验证安装

在 Claude Code 中运行 `/plugin` 或 `/plugin list` 确认插件已安装。

## 使用方法

安装后，当您要求 Claude 执行以下操作时，插件会自动激活：

- 编写 Python 代码
- 创建 Python 脚本或模块
- 重构 Python 代码
- 生成 Python 函数或类
- **审查现有 Python 代码**

### 示例提示

**代码生成：**
```
"写一个解析 JSON 文件的 Python 函数"

"创建一个数据库连接的 Python 类"

"重构这段 Python 代码使其更简洁"
```

**代码审查：**
```
"审查这个 Python 文件：/path/to/file.py"

"检查这段 Python 代码的风格问题"
```

Claude 将自动应用 Python 风格指南规则，包括：

- 正确的命名规范（函数用 `snake_case`，类用 `CapWords`）
- 包含 Args、Returns、Raises 部分的文档字符串
- 正确的导入排序（标准库 → 第三方库 → 本地库）
- 4 空格缩进和 80 字符行限制
- 函数签名的类型提示

### 代码审查输出示例

审查代码时，Claude 提供结构化反馈：

```markdown
## 代码审查摘要

### ✅ 优点
- 函数命名清晰，使用 snake_case
- 类型提示使用良好

### ⚠️ 发现的问题

#### 问题 1：文档 - 缺少文档字符串
- **位置**：第 5 行
- **问题**：函数 `process_data` 缺少文档字符串
- **建议**：添加包含 Args/Returns/Raises 部分的文档字符串

#### 问题 2：风格 - 可变默认参数
- **位置**：第 10 行
- **问题**：`def func(items=[])` 使用了可变默认值
- **建议**：使用 `items=None` 并在函数内部初始化

### 📊 总体评估
- 风格合规性：7/10
- 文档完整性：5/10
- 代码质量：8/10
```

## 兼容性

- **Claude Code**：v1.0.0+
- **Cowork 模式**：完全支持
- **Python 版本**：规则适用于 Python 3.8+

## 风格指南来源

本插件基于广泛采用的 Python 风格规范，包括：

- [PEP 8 – Python 代码风格指南](https://peps.python.org/pep-0008/)
- [PEP 257 – 文档字符串规范](https://peps.python.org/pep-0257/)
- [PEP 484 – 类型提示](https://peps.python.org/pep-0484/)
- [Google Python 风格指南](https://google.github.io/styleguide/pyguide.html)

## 许可证

本插件基于 [MIT 许可证](https://opensource.org/licenses/MIT) 授权。
