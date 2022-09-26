## Excalidraw Plugin Tips

### Sketchnoting

Some rough guidelines on a potential process to sketchnote a book, or a paper, etc.:

1. Read and take notes (Collect - see [[CODE]])
2. Do a single-page chapter/section summary (rough, just for you; [[Work With The Garage Door Up]]) (Organize)
3. Highlight actionable ideas, what can you do with these ideas from the summary? What's next? Followup ideas (Distill)
4. Then, move on to a single-page summary/book-on-a-page (what's the overall structure? Essential details?) (Express)

For the notes that you want to include you can also directly use an image, instead of having to go with the handdrawn drawing option all the time. Make sure to:

- Find an image, e.g., from [Free icons designed by Freepik | Flaticon](https://www.flaticon.com/authors/freepik) for each note and paste directly in the Excalidraw drawing
- You can also draw things directly in Excalidraw of course, make sure to keep them minimal (and atomic)
- Download each image and save it in `Assets/`. Then, you can directly use them upon command, and you can leverage the fuzzy search bar (`Ctrl` + `O`). Additionally, you can follow a naming convention (e.g. suffix with `<XYZ_file_name>-icon`) for more streamlined searching
- You can add and categorize the smaller, atomic drawings in [Excalidraw libraries](https://github.com/excalidraw/excalidraw-libraries#create-your-own-library)
- This means you can also browse the web for premade Excalidraw libraries you can use (and extend)
- You can use emojis with the, already installed, [`Emoji Toolbar`](https://github.com/oliveryh/obsidian-emoji-toolbar) plugin
- Don't try to compose a big drawing all at once; do separate smaller ones, then combine

### General

- You can embed any Excalidraw drawing in a note. Simply create a `[[]]` Obsidian-style reference to the drawing (you can also drag and drop the Excalidraw file). Example: [[Playground.excalidraw]]. Note that when the webpage gets built with MkDocs, because the `Excalidraw/` directory is excluded, the generated links will generate a 404 error. If you also add a exclamation mark directly before the brackets, you can have it rendered inside the note, thanks to the (already installed) [image-in-editor plugin](https://github.com/ozntel/oz-image-in-editor-obsidian). Example: ![[Playground.excalidraw|800]]
- You can turn on the `Grid mode` to help you with aligning objects. Simply right click inside the Excalidraw pane and select `Show grid`
- You can embed $\LaTeX$ expressions: Press `Ctrl` + `P` and search for `Excalidraw: Insert LaTeX formula`
- You can group objects together by selecting them, right clicking and selecting `Group selection`
- You can move objects to different layers, e.g. by right clicking and selecting `Send to back` or `Bring to front`
- You can align objects together by the menu in the laft side of the pane
- You can open a drawing as a separate popup window for more efficient multitasking: `Excalidraw: Create a new drawing - IN A POPUP WINDOW`
- You can refer to [Zsolt's (the plugin author) playlist](https://youtube.com/playlist?list=PL6mqgtMZ4NP1uyKeTs_gu2DIF9xjiGGKs) for more!