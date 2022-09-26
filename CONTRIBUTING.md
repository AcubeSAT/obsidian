- Clone the repository if you haven't already
- Create a new branch
- Work in the new branch
- Open an MR
- ???
- Profit


1. If you're using Windows, make sure to not mess your line endings. I've added an `.editorconfig` file to help, but it'll still let stuff through, depending on if what you're using has [EditorConfig](https://editorconfig.org/) support. So, if you're using Windows, just `git config --global core.autocrlf true`
2. Feel free to use all Obsidian plugins installed liberally. Some things are still missing, for example the Obsidian Admonitions plugin uses different syntax than the MkDocs plugin. In these cases, just use Obsidian syntax and I'll be patching the MkDocs integration here and there to have more things rendered
3. Currently, the Markdown files inside `docs/` (aka the Obsidian Vault) that reside in `Excalidraw` and in `Kanban` are excluded from the website generation using `mkdocs-exclude`. If you want to exclude anything else, `mkdocs.yml` is the place to check
4. If you don't want to add notes but instead want to change something MkDocs-related, or download additional Obsidian plugins or further configure Obsidian, feel free to open a descriptive MR. If you want to further configure Obsidian, please make sure to edit the `LOG.md` appropriately