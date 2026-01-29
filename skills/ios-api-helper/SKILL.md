---
name: ios-api-helper
description: Searches Apple documentation and suggests iOS/SwiftUI best practices during implementation. This skill should be used when user asks "how to implement X in iOS", "what's the API for X", "SwiftUI way to do X", or needs iOS implementation guidance. Triggers on "iOS API", "how to implement", "SwiftUI pattern", "Apple docs", "what API", "UIKit way", "iOS最佳实践", "如何实现", "什么API", "怎么做".
allowed-tools: [mcp__apple-docs__*, Read, Glob, Grep]
---

# iOS API Helper

Guided iOS API lookup and best practice suggestions using Apple documentation.

## When to Use

- User asks "how do I implement X in iOS?"
- User needs to find the right API for a feature
- User wants SwiftUI/UIKit best practices
- Implementing new iOS features

## Workflow

### 1. Understand Intent

Clarify what the user wants to implement:
- UI component? → Check SwiftUI/UIKit options
- System feature? → Find relevant framework
- Data handling? → Core Data, SwiftData, etc.

### 2. Search Apple Docs

```
# Set technology context
mcp__apple-docs__choose_technology(name="SwiftUI")

# Search for relevant symbols
mcp__apple-docs__search_symbols(query="Picker")

# Get detailed documentation
mcp__apple-docs__get_documentation(path="Picker")
```

### 3. Show Examples

Extract code examples from documentation and adapt to user's context.

### 4. Suggest Pattern

Based on project conventions (check `.claude/docs/styles.md` if exists):
- Recommend SwiftUI-native approach first
- Fall back to UIKit if needed
- Consider iOS version compatibility

### 5. Validate

- Check against project's minimum iOS version
- Verify API availability
- Suggest alternatives if needed

## Common Lookups

| User Request | Technology | Symbol |
|--------------|------------|--------|
| "dropdown picker" | SwiftUI | Picker, Menu |
| "list with sections" | SwiftUI | List, Section |
| "pull to refresh" | SwiftUI | refreshable |
| "search bar" | SwiftUI | searchable |
| "bottom sheet" | SwiftUI | sheet, presentationDetents |
| "navigation" | SwiftUI | NavigationStack |
| "async image" | SwiftUI | AsyncImage |
| "app storage" | SwiftUI | AppStorage |

## Integration

Works with:
- `swiftui-patterns` - For architecture guidance
- `ios-build-test` - To verify implementation
- Project `.claude/docs/sdk/*.md` - For project-specific patterns

## Example Session

**User**: "I need to add a dropdown picker for sorting options"

**Skill**:
1. Search: `mcp__apple-docs__search_symbols(query="Picker menu")`
2. Find: `Picker` with `.menu` style
3. Show documentation excerpt
4. Provide code example:

```swift
@State private var selectedSort: SortOption = .newest

Picker("Sort by", selection: $selectedSort) {
    ForEach(SortOption.allCases) { option in
        Text(option.title).tag(option)
    }
}
.pickerStyle(.menu)
```

5. Ask: "Want me to implement this in [detected file]?"

## Notes

- Always check iOS version requirements
- Prefer SwiftUI-native solutions over UIKit bridges
- Reference project conventions from `.claude/docs/` if available
