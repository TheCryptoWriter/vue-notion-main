<div align="center">
  <img src="https://github.com/janniks/vue-notion/raw/main/docs/img/vue-notion.png" alt="vue-notion" width="398px" />
  <p>An unofficial Notion renderer</p>
</div>

<h3 align="center">
  <a href="#features">Features</a>
  <span> ยท </span>
  <a href="#install">Install</a>
  <span> ยท </span>
  <a href="#docs">Docs</a>
  <span> ยท </span>
  <a href="#examples">Examples</a>
  <span> ยท </span>
  <a href="#credits">Credits</a>
</h3>

<p align="center">
  <a href="https://www.npmjs.org/package/vue-notion">
    <img src="https://img.shields.io/npm/v/vue-notion.svg" alt="Package version" />
  </a>
  <a href="https://www.npmjs.org/package/vue-notion">
    <img src="https://img.shields.io/bundlephobia/minzip/vue-notion" alt="Compressed size" />
  </a>
  <a href="https://github.com/janniks/vue-notion/blob/master/LICENSE">
    <img src="https://img.shields.io/badge/license-MIT-blue.svg" alt="MIT license" />
  </a>
  <a href="https://twitter.com/intent/follow?screen_name=jnnksbrt">
    <img src="https://img.shields.io/twitter/url?label=Follow&style=social&url=https%3A%2F%2Ftwitter.com%2Fjnnksbrt" alt="Follow on Twitter" />
  </a>
</p>

---

A Vue renderer for Notion pages.
Use Notion as CMS for your blog, documentation or personal site.

Also check out [react-notion](https://github.com/splitbee/react-notion) (developed by [Splitbee ๐](https://splitbee.io/) โ a fast, reliable, free, and modern analytics for any team)

This package doesn't handle the communication with the API. Check out [notion-api-worker](https://github.com/splitbee/notion-api-worker) from [Splitbee](https://splitbee.io/) for an easy solution.

<sub>Created by <a href="https://twitter.com/jnnksbrt">Jannik Siebert</a></sub>

## Features

๐ฏ **Accurate** โ Results are _almost_ identical

๐จ **Custom Styles** โ Styles are easily adaptable. Optional styles included

๐ฎ **Syntax-Highlighting** โ Beautiful themeable code highlighting using Prism.js

๐ **SSR / Static Generation Support** โ Functions to work with NuxtJS and other frameworks

## Install

### Vue

```bash
npm install vue-notion
```

### NuxtJS Module

Install as a dev-dependency and add `"vue-notion/nuxt"` to the `buildModules` array in `nuxt.config.js`.

```bash
npm install vue-notion --save-dev
```

```js
// nuxt.config.js
export default {
  // ...
  buildModules: ["vue-notion/nuxt"],
};
```

## Docs

- `NotionRenderer`: [`docs/`](https://github.com/janniks/vue-notion/tree/main/docs#notionrenderer)
- Syntax-Highlighting in Code Blocks (with Prism.js): [`docs/`](https://github.com/janniks/vue-notion/tree/main/docs#syntax-highlighting)
- Notion API: [`docs/`](https://github.com/janniks/vue-notion/tree/main/docs#notion-api)
- Nuxt: [`docs/`](https://github.com/janniks/vue-notion/tree/main/docs#nuxtjs--server-side-rendering--static-site-generation)

> Check out a full working demo at [vue-notion.now.sh](https://vue-notion.now.sh/) โจ
> The code for the demo is in [`example/`](https://github.com/janniks/vue-notion/tree/main/example).

## Examples

These examples use a simple wrapper around the [`notion-api-worker`](https://github.com/splitbee/notion-api-worker) to access the Notion page data.
It is also possible to store a page received from the Notion API in `.json` and use it without the `async/await` part.

> Use the `getPageBlocks` and `getPageTable` methods with caution!
> They are based on the private Notion API.
> We can NOT guarantee that it will stay stable.
> The private API is warpped by [notion-api-worker](https://github.com/splitbee/notion-api-worker).
> If you use these methods a lot, please consider hosting you own instance, as described in [`docs#notion-api`](https://github.com/janniks/vue-notion/tree/main/docs#notion-api).

### Basic Example for Vue

This example is a part of [`example/`](https://github.com/janniks/vue-notion/tree/main/example) and is hosted at [vue-notion.now.sh/vue](https://vue-notion.now.sh/vue).

```vue
<template>
  <NotionRenderer :blockMap="blockMap" fullPage />
</template>

<script>
import { NotionRenderer, getPageBlocks } from "vue-notion";

export default {
  components: { NotionRenderer },
  data: () => ({ blockMap: null }),
  async created() {
    // get Notion blocks from the API via a Notion pageId
    this.blockMap = await getPageBlocks("8c1ab01960b049f6a282dda64a94afc7");
  },
};
</script>

<style>
@import "vue-notion/src/styles.css"; /* optional Notion-like styles */
</style>
```

### Basic Example for NuxtJS

This example is a part of [`example/`](https://github.com/janniks/vue-notion/tree/main/example) and is hosted at [vue-notion.now.sh/nuxt](https://vue-notion.now.sh/nuxt).

```vue
<template>
  <NotionRenderer :blockMap="blockMap" fullPage />
</template>

<script>
export default {
  data: () => ({ blockMap: null }),
  async asyncData({ $notion }) {
    // use Notion module to get Notion blocks from the API via a Notion pageId
    const blockMap = await $notion.getPageBlocks(
      "8c1ab01960b049f6a282dda64a94afc7"
    );
    return { blockMap };
  },
};
</script>

<style>
@import "vue-notion/src/styles.css"; /* optional Notion-like styles */
</style>
```

## Sites using vue-notion ๐

List of pages that are using this library.

- [HelpKit](https://www.helpkit.so) โ Build Knowledge Bases in Notion
- [StorePreviewer](https://www.storepreviewer.com) โ Preview and optimize your app store presence
- [Dominik Sobe's Personal Site](https://dominiksobe.com/)
- [Bersihin Tech](https://tech.bersihin.co/)
- [Wisata Diary](https://wisatabook.com/diary)
- [AymaneMx's Blog](https://aymanemx.com/posts/)
- [Notaku](https://notaku.website?ref=vue-notion) โ Build docs and blog websites from Notion pages
- _...if you're using `vue-notion`, we'd be happy to feature you here_

## Supported Blocks

Most common block types are supported. We happily accept pull requests to add support for the missing blocks.

| Block Type        | Supported      | Notes                  |
| ----------------- | -------------- | ---------------------- |
| Text              | โ Yes         |                        |
| Heading           | โ Yes         |                        |
| Image             | โ Yes         |                        |
| Image Caption     | โ Yes         |                        |
| Bulleted List     | โ Yes         |                        |
| Numbered List     | โ Yes         |                        |
| Quote             | โ Yes         |                        |
| Callout           | โ Yes         |                        |
| Column            | โ Yes         |                        |
| iframe            | โ Yes         |                        |
| Video             | โ Yes         | Only embedded videos   |
| Divider           | โ Yes         |                        |
| Link              | โ Yes         |                        |
| Code              | โ Yes         |                        |
| Web Bookmark      | โ Yes         |                        |
| Toggle List       | โ Yes         |                        |
| Page Links        | โ Yes         |                        |
| Cover             | โ Yes         | Enable with `fullPage` |
| Equations         | โ Yes         |                        |
| Checkbox          | โ Yes         |                        |
| Simple Tables     | โ Yes         |                        |
| Databases         | โ Not planned |                        |
| Table Of Contents | โ Not planned |                        |

Please, feel free to [open an issue](https://github.com/janniks/vue-notion/issues/new) if you notice any important blocks missing or anything wrong with existing blocks.

## Credits

- [Jannik Siebert](https://twitter.com/jnnksbrt) โ vue-notion Code
- [Dominik Sobe](https://twitter.com/sobedominik) โ vue-notion Inspiration, Debugging
- [vue-notion Contributors ๐](https://github.com/janniks/vue-notion/graphs/contributors)
- [Tobias Lins](https://tobi.sh) โ react-notion Idea, Code
- [Timo Lins](https://timo.sh) โ react-notion Code, Documentation
- [samwightt](https://github.com/samwightt) โ react-notion Inspiration & API Typings
- [react-notion Contributors ๐](https://github.com/splitbee/react-notion/graphs/contributors)

- Big thanks to [NuxtJS](https://nuxtjs.org) for being awesome!

## License โ๏ธ

MIT ยฉ [Jannik Siebert](https://twitter.com/jnnksbrt)
