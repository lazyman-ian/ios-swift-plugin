# ios-swift-plugin

Comprehensive iOS/Swift development toolkit for Claude Code with skills, commands, agents, and automated validation.

## Features

### Skills (10)

| Skill | Description |
|-------|-------------|
| ios-api-helper | Apple documentation lookup and iOS best practices |
| ios-build-test | Token-efficient xcodebuild commands |
| ios-debugger | Simulator debugging and UI interaction |
| ios-ui-docs | UIKit components and Auto Layout guidance |
| ios-widget-developer | WidgetKit, Timeline Providers, Live Activities |
| swift-concurrency | Swift Concurrency patterns and Swift 6 migration |
| swiftui-expert | SwiftUI best practices and modern APIs |
| swiftui-liquid-glass | iOS 26+ Liquid Glass API |
| swiftui-performance-audit | Performance diagnosis and optimization |
| macos-spm-app-packaging | SwiftPM macOS app bundling and notarization |

### Commands (4)

| Command | Description |
|---------|-------------|
| `/swift-audit [path]` | Scan for concurrency violations |
| `/xcode-test [scheme]` | Quick build and test |
| `/swift-fix-issue <number>` | End-to-end GitHub issue resolution |
| `/app-changelog [from-tag]` | Generate release notes from git |

### Agents (2)

| Agent | Trigger |
|-------|---------|
| concurrency-reviewer | Auto-analyzes Swift files after edits |
| performance-auditor | Auto-checks performance after SwiftUI edits |

### Hooks (2)

| Hook | Type | Description |
|------|------|-------------|
| ConcurrencyGuard | PreToolUse (blocking) | Blocks concurrency anti-patterns |
| SwiftValidator | PostToolUse (async) | Analyzes Swift files after edits |

## Installation

```bash
# Via Claude CLI
claude plugin install ios-swift-plugin

# Or local development
claude --plugin-dir ~/work/ios-swift-plugin
```

## Prerequisites

- Xcode (for build/test commands)
- Apple Documentation MCP (apple-docs)
- Optional: xclaude-plugin (for simulator control)

## ConcurrencyGuard Setup

Build the SwiftSyntax-based static analyzer:

```bash
cd tools/ConcurrencyGuard
swift build -c release
```

The hook will automatically use the built binary.

## Concurrency Rules Enforced

| Code | Rule |
|------|------|
| CC-CONC-001 | Prohibits `Task.detached` |
| CC-CONC-002 | Blocks `Task {}` in initializers |
| CC-CONC-003 | Prevents `Task {}` in render/layout paths |
| CC-CONC-004 | Requires `onTermination` for AsyncStream |
| CC-CONC-005 | Limits concurrent tasks (max 3 per function) |
| CC-CONC-008 | Forbids `.background` priority for `for await` |

## License

MIT
