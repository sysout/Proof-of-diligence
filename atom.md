## [Atom Basics](http://flight-manual.atom.io/getting-started/sections/atom-basics/)

## Shortcuts
- open markdown file preview (`Ctrl Shift M`)
- open search-driven menu (`Cmd Shift P`)
- find file (`Cmd P` or `Cmd T`)
- open settings (`cmd ,`)
- toggle tree view (`cmd \`)
- "Move Line Up" (`Ctrl Cmd Up`)
- "Move Line Down" (`Ctrl Cmd Down`)
-  (`Alt Shift k`)
- delete line (`Ctrl Shift k`)
- toggle git tab (`Ctrl Shift 9`)

## Config
- menu (Atom -> Config...)

## Markdown Writer
- https://github.com/zhuochun/md-writer/wiki/Settings
- [enable shortcuts](https://github.com/zhuochun/md-writer/wiki/Settings-for-Keymaps)
- **Continue lists or table rows** when you press `enter` ([customize][adaa9527]).
  - **Correct ordered list numbers** (`markdown-writer:correct-order-list-numbers`).
- **Insert link** (`shift-cmd-k`) and **automatically link to the text next time**.
  - Insert inline link.
  - Insert reference link with title. _Use `-` in title field to create an empty title reference link._
  - Remove link (and its reference) after URL is deleted.
  - Search published posts by title in your blog.f
- **Insert footnote** (`markdown-writer:insert-footnote`), and edit footnote labels.
- **Insert image from file or clipboard** (`shift-cmd-i`), preview image and able to copy image to your blog's images directory.
- **Insert table** (`markdown-writer:insert-table`), and quick **jump to next table cell** (`cmd-j cmd-t`).
- **Format table** (`markdown-writer:format-table`) with table alignments.
- **Toggle headings**: `ctrl-alt-[1-5]` to switch among `H1` to `H5`.
- **Toggle text styles** ([customize styles][7ddaeaf4]):
  - `code` (`cmd-'`)
  - **bold** (`cmd-b`)
  - _italic_ (`cmd-i`)
  - ~~strike through~~ (`cmd-h`)
  - `'''code block'''` (`shift-cmd-"`)
  - `<kbd>key</kbd>` (`cmd + k`)
  - `- unordered list` (`shift-cmd-U`)
  - `0. ordered list` (`shift-cmd-O`)
  - `> blockquote` (`shift-cmd->`)
  - `- [ ] task list` (`markdown-writer:toggle-task`)
- **Jumping commands**:
  - Jump to previous heading (`cmd-j cmd-p`)
  - Jump to next heading (`cmd-j cmd-n`)
  - Jump to next table cell (`cmd-j cmd-t`)
  - Jump to reference marker/definition (`cmd-j cmd-d`)
- **Open link under cursor in browser** (`markdown-writer:open-link-in-browser`), and works on reference links.
- **Markdown cheat sheet** (`markdown-writer:open-cheat-sheet`).
- **Toolbar for Markdown Writer** is available at [tool-bar-markdown-writer][82a2aced].
- **AsciiDoc support** with [language-asciidoc][2f0cb1f9].

  [82a2aced]: https://atom.io/packages/tool-bar-markdown-writer "Toobar for Markdown Writer"
  [2f0cb1f9]: https://atom.io/packages/language-asciidoc "AsciiDoc Language Package for Atom"
  [adaa9527]: https://github.com/zhuochun/md-writer/wiki/Settings#use-different-unordered-list-styles "Customizations"

## [Document Outline](https://atom.io/packages/document-outline)
## [atom-shortcuts package](https://atom.io/packages/atom-shortcuts)
## [markdown-scroll-sync Atom editor package](https://atom.io/packages/markdown-scroll-sync)
