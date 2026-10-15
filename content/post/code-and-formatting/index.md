+++
title = 'Code and Formatting'
date = '2026-01-03T10:00:00Z'
description = 'Syntax highlighting and Markdown basics'
tags = ['example', 'markdown']
topics = ['Getting started']
+++

Code blocks are highlighted by Hugo when the site is built, so no JavaScript is needed.

<!--more-->

## Code

```bash
hugo new content post/my-first-post
hugo server --buildDrafts
```

```go
package main

import "fmt"

func main() {
	fmt.Println("Hello from Hugo")
}
```

Inline code looks like `git status`.

## Lists and quotes

- Item one
- Item two

1. First
2. Second

> A quote.

## Tables

| Command | What it does |
|---------|--------------|
| `hugo` | Builds the site into `public/` |
| `hugo server` | Serves the site at http://localhost:1313 |
