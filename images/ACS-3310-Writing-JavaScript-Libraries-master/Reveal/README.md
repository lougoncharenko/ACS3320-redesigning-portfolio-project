# reveal-md

## Quick start

Run Slides with: 

```bash
reveal-md Lessons/ --css makeschool.css
reveal-md Lessons/ --static Slides
reveal-md Lessons/ --static Slides --css makeschool.css
```

## Installation:

```bash
npm install -g reveal-md
```

## Usage:

### Syntax

**Slide styling:**

```
<!-- .slide: data-background="./Images/header.svg" data-background-repeat="none" data-background-size="40% 40%" data-background-position="center 10%" class="header" -->
```

**Change background color:**

```
<!-- .slide: data-background="#087CB8" -->
```

**Signal a horizontal slide transition**

```
<!-- > -->
```

**Signal a vertical slide transition**

```
<!-- v -->
```

### Local Presentation

This starts a local server and opens any Markdown file as a reveal.js presentation in the default browser.

```bash
reveal-md Lessons/

reveal-md Lessons/ --theme solarized

reveal-md Lessons/ --css makeschool.css
```

### Generate Slides

Generate static HTML (for GitHub Pages):

```bash
reveal-md Lessons/ --static Slides

reveal-md Lessons/ --static Slides --theme solarized

reveal-md Lessons/ --static Slides --css makeschool.css
```

## Resources
For more information, check out the [reveal-md documentation](https://github.com/webpro/reveal-md).