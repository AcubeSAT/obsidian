<div align="center">
<p>
    <a href="https://spacedot.gr/">SpaceDot 🌌🪐</a> &bull;
    <a href="https://acubesat.spacedot.gr/">AcubeSAT 🛰️🌎</a>
</p>
</div>

## Description

https://acubesat.gitlab.io/documentation/obsidian/

This repository hosts a complete [Obsidian](https://obsidian.md/) [vault](https://gitlab.com/acubesat/documentation/obsidian/-/tree/main/docs), together with plugins, configuration, etc.
As some [SpaceDot](https://spacedot.gr/) members are starting to experiment with using Obsidian for notetaking in the scope of the [AcubeSAT](https://acubesat.spacedot.gr/) project, this is an attempt to gather everything in a single, centralized knowledge base.
Additionally, this repository contains all the necessary files for [MkDocs](https://www.mkdocs.org/) [integration](https://gitlab.com/acubesat/documentation), using [GitLab CI](https://docs.gitlab.com/ee/ci/).
This allows for automatically building and deploying a [website](https://acubesat.gitlab.io/documentation/obsidian/) generated by the markdown notes, through [GitLab Pages](https://docs.gitlab.com/ee/user/project/pages/):

![index-example][index-example]

[index-example]: assets/webpage/example-index.png "Example index page layout"

## Table of Contents

<details>
<summary>Click to expand</summary>

[[_TOC_]]

</details>

## Features

The repository hosts two different things: the Obsidian vault itself, and the configuration related to generating and deploying the webpage.

### Obsidian

The theme currently used is [colineckert/obsidian-things: An Obsidian theme inspired by the beautifully-designed app, Things.(https://github.com/colineckert/obsidian-things), in `Dark` mode.

#### Plugins

Community plugins:

[valentine195/obsidian-admonition](https://github.com/valentine195/obsidian-admonition): Adds admonition block-styled content to Obsidian

![plugin-admonition][plugin-admonition]

[tgrosinger/advanced-tables-obsidian](https://github.com/tgrosinger/advanced-tables-obsidian): Improved table navigation, formatting, and manipulation in Obsidian

![plugin-advanced-tables][plugin-advanced-tables]

[GitHub - zolrath/obsidian-auto-link-title](https://github.com/zolrath/obsidian-auto-link-title): Automatically fetch the titles of pasted links

![plugin-auto-link-title][plugin-auto-link-title]

[hans/obsidian-citation-plugin](https://github.com/hans/obsidian-citation-plugin): Obsidian plugin which integrates your academic reference manager with the Obsidian editor. Search your references from within Obsidian and automatically create and reference literature notes for papers and books.

![plugin-citation][plugin-citation]

[oliveryh/obsidian-emoji-toolbar](https://github.com/oliveryh/obsidian-emoji-toolbar): Quickly search for and add emojis to your editor

![plugin-emoji-toolbar][plugin-emoji-toolbar]

[zsviczian/obsidian-excalidraw-plugin](https://github.com/zsviczian/obsidian-excalidraw-plugin): A plugin to edit and view Excalidraw drawings in Obsidian

![plugin-excalidraw][plugin-excalidraw]

[nothingislost/obsidian-hover-editor](https://github.com/nothingislost/obsidian-hover-editor): Transform the Page Preview hover into a working editor instance

![plugin-hover-editor-1][plugin-hover-editor-1]
![plugin-hover-editor-2][plugin-hover-editor-2]

[mgmeyers/obsidian-kanban](https://github.com/mgmeyers/obsidian-kanban): Create markdown-backed Kanban boards in Obsidian.

![plugin-kanban][plugin-kanban]

[denolehov/obsidian-git](https://github.com/denolehov/obsidian-git): Backup your Obsidian vault with git

![plugin-git][plugin-git]

[ozntel/oz-image-in-editor-obsidian](https://github.com/ozntel/oz-image-in-editor-obsidian): This Obsidian plugin to view Images, Transclusions, iFrames and PDF Files within the Editor without a necessity to switch to Preview.

![plugin-image-in-editor][plugin-image-in-editor]

[denolehov/obsidian-url-into-selection](https://github.com/denolehov/obsidian-url-into-selection): Paste URLs into selected text "notion style"

![plugin-url-into-selection][plugin-url-into-selection]

[deathau/sliding-panes-obsidian](https://github.com/deathau/sliding-panes-obsidian): Andy Matuschak Mode as a plugin

![plugin-sliding-panes][plugin-sliding-panes]

[plugin-admonition]: assets/plugins/admonition.png "Obsidian Admonition plugin"
[plugin-advanced-tables]: assets/plugins/advanced-tables.png "Obsidian Admonition plugin"
[plugin-auto-link-title]: assets/plugins/auto-link-title.png "Obsidian Admonition plugin"
[plugin-citation]: assets/plugins/citation.png "Obsidian Admonition plugin"
[plugin-emoji-toolbar]: assets/plugins/emoji-toolbar.png "Obsidian Admonition plugin"
[plugin-excalidraw]: assets/plugins/excalidraw.png "Obsidian Admonition plugin"
[plugin-hover-editor-1]: assets/plugins/hover-editor-1.png "Obsidian Admonition plugin"
[plugin-hover-editor-2]: assets/plugins/hover-editor-2.png "Obsidian Admonition plugin"
[plugin-kanban]: assets/plugins/kanban.png "Obsidian Admonition plugin"
[plugin-git]: assets/plugins/git.png "Obsidian Admonition plugin"
[plugin-image-in-editor]: assets/plugins/image-in-editor.png "Obsidian Admonition plugin"
[plugin-url-into-selection]: assets/plugins/url-into-selection.png "Obsidian Admonition plugin"
[plugin-sliding-panes]: assets/plugins/sliding-panes.png "Obsidian Admonition plugin"

### Webpage

![search-example][search-example]

[search-example]: assets/webpage/example-search.png "Example search bar layout"

#### MkDocs

Built-in Markdown extensions:

- [footnotes](https://squidfunk.github.io/mkdocs-material/reference/footnotes/)
- [attr_list](https://squidfunk.github.io/mkdocs-material/setup/extensions/python-markdown/#attribute-lists)
- [pymdownx.highlight](https://facelessuser.github.io/pymdown-extensions/extensions/highlight/)
- [pymdownx.superfences](https://facelessuser.github.io/pymdown-extensions/extensions/superfences/)
- [pymdownx.details](https://facelessuser.github.io/pymdown-extensions/extensions/details/)
- [pymdownx.magiclink](https://facelessuser.github.io/pymdown-extensions/extensions/magiclink/)
- [pymdownx.tasklist](https://facelessuser.github.io/pymdown-extensions/extensions/tasklist/)
- [pymdownx.emoji](https://facelessuser.github.io/pymdown-extensions/extensions/emoji/)
- [admonition](https://squidfunk.github.io/mkdocs-material/reference/admonitions/)
- [toc](https://python-markdown.github.io/extensions/toc/)

Community plugins:

- [search](https://www.mkdocs.org/user-guide/configuration/#search)
- [roamlinks](https://github.com/Jackiexiao/mkdocs-roamlinks-plugin)
- [exclude:](https://github.com/apenwarr/mkdocs-exclude)
