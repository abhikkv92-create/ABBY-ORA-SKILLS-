---
name: refactor-assist
description: Analyzes code for common anti-patterns, code smells, and suggests refactoring opportunities. Provides targeted improvement suggestions with effort estimates.
model: sonnet
effort: medium
maxTurns: 10
---

# /refactor-assist

Detects code smells and suggests refactoring improvements.

## Usage

```
/refactor-assist [--path PATH] [--severity high|medium|low] [--auto-fix]
```

## Analysis Categories

### 1. Code Structure Issues
- **Long functions**: > 50 lines - split into smaller units
- **Deep nesting**: > 4 levels - extract conditions
- **Too many parameters**: > 4 - use objects or options
- **Duplicate code**: Extract to shared functions
- **Dead code**: Unused code to remove

### 2. Naming Issues
- **Single-letter variables**: Use meaningful names
- **Inconsistent naming**: snake_case vs camelCase
- **Magic numbers**: Define as named constants
- **Vague names**: foo, bar, temp - rename clearly

### 3. Complexity Issues
- **Cyclomatic complexity**: High branching - simplify
- **Large files**: > 500 lines - split modules
- **Tight coupling**: Excessive dependencies
- **Feature envy**: Method accessing other objects extensively

### 4. Architectural Issues
- **God objects**: Objects doing too much
- **Circular dependencies**: Restructure imports
- **Hidden dependencies**: Unclear requirements
- **Shotgun surgery**: Changes require scattered updates

### 5. Anti-Patterns
- **Switch statements**: Use polymorphism
- **Type checking**: Use polymorphism or generics
- **Premature optimization**: Optimize when needed
- **Yeast code**: Unnecessary abstraction

## Severity Levels

| Level | Threshold | Action Required |
|------|-----------|----------------|
| 🔴 High | Security risk, bugs, performance | Immediate fix |
| 🟡 Medium | Maintainability, clarity | Plan fix |
| 🟢 Low | Style, convention | Consider fix |

## Output Format

```
🔍 REFACTOR ANALYSIS

Path: [analyzed path]
Files: [N] scanned
Issues Found: [N total]

🔴 High: [count]
🟡 Medium: [count]
🟢 Low: [count]

📋 TOP ISSUES:

1. [file:line] - [issue description]
   Severity: [level]
   Effort: [small|medium|large]
   Suggestion: [refactoring approach]

2. [file:line] - [issue description]
   ...
```

## Auto-Fix Mode

With `--auto-fix`:
- Automatic fixes for safe improvements
- Renaming variables
- Extracting constants
- Simple refactorings
- Prompts for complex changes

## Examples

```
/refactor-assist                    # Full scan
/refactor-assist --path src/utils   # Focus on utils
/refactor-assist --severity high     # Critical issues only
/refactor-assist --auto-fix          # Apply safe fixes
```