+++
title = 'Hello World'
date = '2026-01-02T10:00:00Z'
description = 'An example post stored as a page bundle'
tags = ['example', 'images']
topics = ['Getting started']
+++

This post is a page bundle: a folder holding `index.md` and the images it uses.
Delete it once you have written your own posts.

<!--more-->

## Images

`sample.png` is 1600px wide. The `img` shortcode scales it down to 800px at build time:

{{< img src="sample.png" alt="Sample image" width="800" caption="Resized from 1600px to 800px" >}}

The source:

```text
{{</* img src="sample.png" alt="Sample image" width="800" caption="Resized from 1600px to 800px" */>}}
```

## YouTube

Hugo has a built-in shortcode for videos:

```text
{{</* youtube VIDEO_ID */>}}
```
