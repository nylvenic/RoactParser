# Roact Snippet Parser

A small TypeScript parser used to convert a shorthand Roact DSL into
nested `Roact.createElement` snippet output. Designed for use in editor
tooling (e.g. VS Code extensions).

## Grammar Overview

- `>` denotes a parent → child relationship
- `+` denotes sibling relationships
- `*n` multiplies elements (e.g., `*2` creates two instances)
- `{text}` generates a `Text` prop
- `[key=value]` defines props (comma-separated for multiple props)

Example:

```
Roact.Frame>TextLabel{Hello}+TextButton*2
```

## Example

Input:

```
Roact.Frame>TextLabel{Hello}+TextButton*2
```

Output:

```lua
Roact.createElement("Frame", {}, {
    Roact.createElement("TextLabel", { Text = "Hello" }, {}),
    Roact.createElement("TextButton", {}, {}),
    Roact.createElement("TextButton", {}, {}),
})
```

## Usage

```ts
const parser = new RoactParser();
parser.parse(input);
const snippet = parser.toSnippet();
```

## Context

This parser was developed as the core parsing logic for a VS Code extension
providing Roact snippet generation and syntax assistance.

The extension itself is not open-sourced, but this repository represents
the reusable parsing and tree-construction logic written by the author.

## License

MIT
