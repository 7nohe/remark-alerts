# remark-alerts

[remark](https://github.com/remarkjs/remark) plugin to support GitHub-style alerts.

This project is a fork of the [antfu/markdown-it-github-alerts](https://github.com/antfu/markdown-it-github-alerts) project.


> [!NOTE]
> Highlights information that users should take into account, even when skimming.

> [!TIP]
> Optional information to help a user be more successful.

> [!IMPORTANT]
> Crucial information necessary for users to succeed.

> [!WARNING]
> Critical content demanding immediate user attention due to potential risks.

> [!CAUTION]
> Negative potential consequences of an action.

```
> [!NOTE]
> Highlights information that users should take into account, even when skimming.

> [!TIP]
> Optional information to help a user be more successful.

> [!IMPORTANT]
> Crucial information necessary for users to succeed.

> [!WARNING]
> Critical content demanding immediate user attention due to potential risks.

> [!CAUTION]
> Negative potential consequences of an action.
```

## Usage

```bash
npm i remark-alerts
```

```js
import { unified } from "unified";
import remarkHtml from "remark-html";
import remarkParse from "remark-parse";
import remarkAlerts from 'remark-alerts'

const content = `
# Hello

> [!NOTE]
> Highlights information that users should take into account, even when skimming.

> [!TIP]
> Optional information to help a user be more successful.

> [!IMPORTANT]
> Crucial information necessary for users to succeed.

> [!WARNING]
> Critical content demanding immediate user attention due to potential risks.

> [!CAUTION]
> Negative potential consequences of an action.

`

const parsedContent = await unified()
  .use(remarkParse)
  .use(remarkAlerts)
  .use(remarkHtml, { sanitize: false })
  .process(content);

console.log(parsedContent)

```

For the options available, please refer to [the jsdoc](./src/index.ts).

## Functionality

This plugin transforms the following markdown:

```markdown
> [!NOTE]
> Highlights information that users should take into account, even when skimming.
```

to the following HTML:

```html
<div class="markdown-alert markdown-alert-note">
  <p class="markdown-alert-title" dir="auto"><!-- svg icon-->Note</p><p>
  Highlights information that users should take into account, even when skimming.</p>
</div>
```

Which is compatible with the GitHub's output.

### Styling

You can write your custom styles for your alerts.

We also provide some CSS extracted from GitHub's styles for you to use.

```js
import 'remark-alerts/styles/github-colors-light.css'
import 'remark-alerts/styles/github-colors-dark-media.css'
import 'remark-alerts/styles/github-base.css'
```

You might change `github-colors-dark-media.css` to `github-colors-dark-class.css` if you are using class-based (`.dark`) dark mode.

Refer to the [source code](./styles) for more details.

### Customization

In order to also support [Obsidian callouts syntax](https://help.obsidian.md/Editing+and+formatting/Callouts) it is possible to allow any type of markers with the following setting:

```js
unified().use(remarkAlerts, { markers: "*" })
```
Alternative titles are also supported, by appending it to the marker like this:

```markdown
> [!note] Nota bene
> The custom title will replace the regular title.
```

## License

MIT
