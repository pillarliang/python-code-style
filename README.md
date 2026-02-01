# Python Code Style Plugin

**Language / 语言**: [English](README.md) | [中文简体](docs/README.zh-cn.md) | [繁體中文](docs/README.zh-tw.md) | [Deutsch](docs/README.de.md) | [Français](docs/README.fr.md) | [Italiano](docs/README.it.md) | [日本語](docs/README.ja.md) | [한국어](docs/README.ko.md) | [Português](docs/README.pt.md) | [Español](docs/README.es.md)

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Claude Code Plugin](https://img.shields.io/badge/Claude%20Code-Plugin-blue.svg)](https://code.claude.com/docs/en/plugins)

A Claude Code plugin that enforces professional Python style guidelines for all Python code generation.

## Features

- **Automatic Activation**: Claude automatically follows Python style guidelines when generating or reviewing code
- **Code Review Support**: Review existing Python code with detailed feedback and scoring
- **Comprehensive Coverage**: Includes industry-standard best practices
  - Naming conventions (modules, classes, functions, variables, constants)
  - Docstring format with Args, Returns, Raises, Yields sections
  - Import rules and ordering
  - Formatting standards (indentation, line length, whitespace)
  - Language rules (exceptions, type hints, comprehensions)
- **Detailed References**: Supporting documentation for edge cases

## Installation

### Method 1: Via Marketplace (Recommended)

In Claude Code, run:

```bash
# Step 1: Add the marketplace
/plugin marketplace add pillarliang/python-code-style

# Step 2: Install the plugin
/plugin install python-code-style
```

### Method 2: Via settings.json

Add to your `~/.claude/settings.json`:

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

### Method 3: Manual Installation

```bash
# Clone the repository
git clone https://github.com/pillarliang/python-code-style.git

# Copy to Claude plugins directory
cp -r python-code-style ~/.claude/plugins/python-code-style
```

### Verify Installation

Run `/plugin` or `/plugin list` in Claude Code to confirm the plugin is installed.

## Usage

Once installed, the plugin activates automatically whenever you ask Claude to:

- Write Python code
- Create Python scripts or modules
- Refactor Python code
- Generate Python functions or classes
- **Review existing Python code**

### Example Prompts

**Code Generation:**
```
"Write a Python function to parse JSON files"

"Create a Python class for database connections"

"Refactor this Python code to be cleaner"
```

**Code Review:**
```
"Review this Python file: /path/to/file.py"

"Check this Python code for style issues"
```

Claude will automatically apply Python style guide rules, including:

- Proper naming conventions (`snake_case` for functions, `CapWords` for classes)
- Docstrings with Args, Returns, Raises sections
- Correct import ordering (stdlib → third-party → local)
- 4-space indentation and 80-character line limits
- Type hints for function signatures

### Example Output

```python
"""User authentication module.

This module provides utilities for user authentication and session
management.
"""

from __future__ import annotations

import hashlib
import secrets
from typing import TYPE_CHECKING

if TYPE_CHECKING:
    from collections.abc import Mapping

# Constants
DEFAULT_TIMEOUT_SECONDS = 3600
MAX_LOGIN_ATTEMPTS = 5


class AuthenticationError(Exception):
    """Raised when authentication fails."""


def hash_password(password: str, salt: str | None = None) -> tuple[str, str]:
    """Hash a password with optional salt.

    Args:
        password: The plaintext password.
        salt: Optional salt. Generated if not provided.

    Returns:
        A tuple containing (password_hash, salt).

    Raises:
        ValueError: If password is empty.
    """
    if not password:
        raise ValueError("Password cannot be empty")

    if salt is None:
        salt = secrets.token_hex(16)

    salted_password = f"{salt}{password}"
    password_hash = hashlib.sha256(salted_password.encode()).hexdigest()

    return password_hash, salt
```

### Code Review Example Output

When reviewing code, Claude provides structured feedback:

```markdown
## Code Review Summary

### ✅ What's Good
- Clear function naming using snake_case
- Good use of type hints

### ⚠️ Issues Found

#### Issue 1: Documentation - Missing docstring
- **Location**: Line 5
- **Problem**: Function `process_data` lacks a docstring
- **Suggestion**: Add docstring with Args/Returns/Raises sections

#### Issue 2: Style - Mutable default argument
- **Location**: Line 10
- **Problem**: `def func(items=[])` uses mutable default
- **Suggestion**: Use `items=None` and initialize inside function

### 📊 Overall Assessment
- Style Compliance: 7/10
- Documentation: 5/10
- Code Quality: 8/10
```

## Plugin Structure

```
python-code-style/
├── .claude-plugin/
│   └── plugin.json              # Plugin manifest
├── skills/
│   └── python-code-style/
│       ├── SKILL.md             # Core skill definition
│       └── references/
│           ├── language-rules.md    # Python language rules
│           ├── style-rules.md       # Formatting and style rules
│           ├── naming-conventions.md # Naming convention details
│           └── docstrings.md        # Docstring format guide
└── README.md                    # This file
```

## Skill Contents

### SKILL.md (Core)

Quick reference including:
- Naming conventions table
- Essential formatting rules
- Docstring format template
- Import order
- Code generation checklist
- **Code review checklist** (naming, documentation, style, code quality)
- **Standardized review output format**

### Reference Files

| File | Content |
|------|---------|
| `language-rules.md` | Lint, imports, exceptions, global state, comprehensions, generators, lambda, type annotations |
| `style-rules.md` | Semicolons, line length, indentation, blank lines, whitespace, comments, strings, logging |
| `naming-conventions.md` | Complete naming rules with examples for all Python constructs |
| `docstrings.md` | Full docstring format for modules, classes, functions with Args/Returns/Raises/Yields |

## Customization

### Extending the Plugin

You can customize the plugin by editing files in the `skills/python-code-style/` directory:

1. **Modify rules**: Edit `SKILL.md` to add or change rules
2. **Add references**: Create new `.md` files in `references/`
3. **Override defaults**: Update specific sections to match your team's preferences

### Creating a Fork

```bash
# Fork and clone
git clone https://github.com/pillarliang/python-code-style.git

# Make your changes
cd python-code-style
# Edit files...

# Install your customized version
cp -r . ~/.claude/plugins/python-code-style
```

## Compatibility

- **Claude Code**: v1.0.0+
- **Cowork Mode**: Fully supported
- **Python Versions**: Rules apply to Python 3.8+

## Style Guide Sources

This plugin is based on widely-adopted Python style conventions including:

- [PEP 8 – Style Guide for Python Code](https://peps.python.org/pep-0008/)
- [PEP 257 – Docstring Conventions](https://peps.python.org/pep-0257/)
- [PEP 484 – Type Hints](https://peps.python.org/pep-0484/)
- [Google python styleguide](https://google.github.io/styleguide/pyguide.html)

## License

This plugin is licensed under the [MIT License](https://opensource.org/licenses/MIT).

## Contributing

Contributions are welcome! Please:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/improvement`)
3. Commit your changes (`git commit -am 'Add new feature'`)
4. Push to the branch (`git push origin feature/improvement`)
5. Open a Pull Request

## Changelog

### v1.0.0

- Initial release
- Comprehensive Python style guide coverage
- Naming conventions, docstrings, imports, formatting rules
- Detailed reference documentation
