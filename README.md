# latex-environment

## Overview

This is Quarto extension that enables `divs` to be output as a custom environment in LaTeX. This is useful when you'd like to share content between LaTeX and other formats, but need the content to be placed in an environment when emitting LaTeX.

## Installation

To install this extension in your current directory (or into the Quarto project that you're currently working in),  use the following command:

```
quarto install extension quarto-ext/latex-environment
```

## Usage

### Environments

Divs with a class name listed in the in the `environments` key will be emitted in LaTeX as an environment with the provided name (or the class name itself if no name is provided). All of the following are valid:

```yaml
environments: center
```

```yaml
environments: [center]
```

```yaml
environments:
  center: center-env
```

#### Example

```markdown
---
title: LaTeX Environment
format:
   pdf: default
   html: default
filters:
   - latex-environment
environments: [center]
---

::: {.center}
The contents of this div will be output in a `center`
LaTeX environment, but will appear in HTML (and any other output 
format as a simple div with the class `center`)
:::
```


#### Options and Arguments

In addition, you may specify options and arguments for the environment as attributes of the div. For example:

```markdown
::: {.foo options="option" arguments="argument"}
body
:::
```

would transform to:

```tex
\begin{foo}[option]{argument}
body
\end{foo}
```


### Commands

Spans with a class name listed in the in the `commands` key will be emitted in LaTeX as a command with the provided name (or the class name itself if no name is provided). All of the following are valid:

```yaml
commands: ce
```

```yaml
command: [ce]
```

```yaml
commands:
  ce: ce-command
```

## Example

```markdown
---
title: LaTeX Command
format:
   pdf:
     include-in-header: 
       text: |
         \usepackage{mhchem}
   html: default
filters:
   - latex-environment
commands: [ce]
---

This will replace spans of class `ce` with the `\ce{}` command for LaTeX output, 
but leave the spans intact for HTML output. So `[H2SO4]{.ce}` becomes [H2SO4]{.ce}.

```

### Options

You may also provide options for commands using the `options` attribute. For example:

```
[Content]{.command options="option1"}
```

generates the following:

```
\command[option1]{Content}
```
