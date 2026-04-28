---
name: project-onboard
description: Auto-detects the technology stack, dependencies, and project structure of the current codebase. Provides a comprehensive tech profile including frameworks, languages, package managers, build tools, and key configuration files.
model: sonnet
effort: medium
maxTurns: 5
triggers:
  - project tech stack
  - what tech
  - detect stack
  - what framework
allowed-tools:
  - Bash
  - Glob
  - Grep
  - Read
---

# /project-onboard

Automatically detects and profiles the technology stack of the current project.

## Usage

```
/project-onboard
```

## Detection Process

### Step 1: Language Detection
- Detect primary language(s) from file extensions
- Check for version files (.java-version, .nvmrc, etc.)

### Step 2: Package Manager Detection
- npm/yarn/pnpm → Node.js projects
- pip/poetry/conda → Python projects
- Maven/Gradle → Java projects
- Cargo → Rust projects
- Go modules → Go projects

### Step 3: Framework Detection
- React/Vue/Angular → Frontend frameworks
- Express/FastAPI/Django → Backend frameworks
- Spring Boot → Enterprise Java
- Next.js/Remix → Full-stack

### Step 4: Build Tool Detection
- webpack/vite/esbuild → Frontend build
- tsc/esbuild/swiftc → Compilers
- make/docker → Build systems

### Step 5: Configuration Discovery
- Linting (ESLint, Pylint, etc.)
- Testing (Jest, Pytest, JUnit, etc.)
- CI/CD (GitHub Actions, Jenkins, etc.)

## Output Format

```
📊 TECH STACK PROFILE

Languages: [list]
Package Manager: [manager] [version]
Frameworks: [list]
Build Tools: [list]
Testing: [list]
Linting: [list]
CI/CD: [list]

🔑 Key Files:
- [config files found]
- [entry points]

📦 Dependencies: [count] packages
```

## Examples

- Auto-detects Node.js + Express + TypeScript + Jest stack
- Auto-detects Python + FastAPI + SQLAlchemy + Pytest stack
- Auto-detects Java + Spring Boot + Maven + JUnit stack