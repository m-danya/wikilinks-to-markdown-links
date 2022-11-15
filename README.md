## WikiLinks to Markdown Links converter

This script converts WikiLinks to Markdown Links. Useful when moving from Obsidian to smth else like VimWiki. It took me more than 2 hours to find all markdown-syntax-breaking cases and implement it in regex:

| **WikiLinks** | **Markdown Links** | **Note** |
|---|---|---|
|` [[Some article \| Custom link name]]` | `[Custom link name](Some article)` | Base case. Spaces near the "\|" should be erased |
|` [[Some article]]` |` [Some article](Some article)` | If a link does not have a custom link name, use its main text |
|` [[Some article with (parentheses) \| Custom link name]` | `[Custom link name](Some article with - parentheses)` | Parantheses break the markdown links. They should be replaced. Files should be renamed! |
|` [[Some article with (parentheses)]` | `[Some article with - parentheses](Some article with - parentheses)` | Same, but with custom link name |
|` [[Article. with. dots]]` |` [Article - with - dots](Article - with - dots)` | Dots also break the markdown links! Files also should be renamed. |
|` [[Article. with. dots \| Custom link name]]` |` [Article - with - dots](Custom link name)` | Same, but without link name |

### Usage:
1. Move the script next to the directory with `.md` files (see Limitations)
2. Run the script:
```bash
./w-to-m.sh
```

### Limitations
1. It is assumed that there is no more than one parentheses pair in each filename
2. It is assumed that there is no more that 5 dots in each filename (excluding dot in ".md")
3. The script can't work properly with nested folders: "rename" will trigger on any dots in path
4. I've completly forgotten what each regexp does and how

