---
name: codebase-map
description: Generates architecture documentation by analyzing the codebase structure, dependencies, and relationships between components. Creates visual and text-based architecture docs.
model: sonnet
effort: medium
maxTurns: 10
---

# /codebase-map

Analyzes and documents the architecture of the current project.

## Usage

```
/codebase-map [--depth N] [--format markdown|json|plantuml]
```

## Analysis Process

### Step 1: Directory Structure Analysis
- Identify root-level directories
- Analyze module boundaries
- Detect monorepo vs single package

### Step 2: Dependency Graph
- Parse package.json, pyproject.toml, pom.xml, etc.
- Build dependency tree
- Identify circular dependencies
- Find unlisted dependencies

### Step 3: Entry Points
- API routes/endpoints
- CLI entry points
- Main application entry
- Test entry points

### Step 4: Component Mapping
- Identify distinct components (services, libraries, modules)
- Map component responsibilities
- Detect coupling patterns
- Find shared code

### Step 5: Architecture Pattern Detection
- MVC/MTV patterns
- Microkernel architecture
- Microservices boundaries
- Domain-driven design boundaries

## Output Format

### Architecture Summary
```
🏗️ CODEBASE MAP

Project: [name]
Type: [monorepo|package|module]
Structure:
├── [directory tree]

📦 Dependencies: [N] direct, [N] transitive
🔄 Circular: [count] detected

🗺️ Component Architecture:
- [Component 1]: [responsibility]
- [Component 2]: [responsibility]

🔗 Key Relationships:
- [Component] → [depends on Component]
```

### Component Detail (--detail)
For each component:
- Files and their roles
- Public API surface
- Configuration requirements
- Test coverage

## Options

| Option | Description |
|--------|-------------|
| `--depth N` | Directory depth to traverse (default: 3) |
| `--format` | Output format: markdown, json, plantuml |
| `--filter` | Focus on specific component |

## Examples

```
/codebase-map                    # Full analysis
/codebase-map --depth 2        # Shallow analysis
/codebase-map --format json    # JSON output
/codebase-map --filter api     # Focus on API component
```