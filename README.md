# Welcome to [Slidev](https://github.com/slidevjs/slidev)!

To start the slide show:

- If you use nvm, run `nvm use` first to activate the version specified in `.nvmrc`.
- `npm install`
- `npm run dev`
- visit <http://localhost:3030>

Edit the [slides.md](./slides.md) to see the changes.

## Export to PDF

Install the Chromium exporter once:

```bash
npm install -D playwright-chromium
```

Then export the slides:

```bash
npm run export
```

The PDF is generated as `slides-export.pdf` in the project root.

Learn more about Slidev at the [documentation](https://sli.dev/).
