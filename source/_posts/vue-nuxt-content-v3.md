---
title: "202501  @nuxt/content v2 升級 v3 筆記"
date: 2025-04-10 18:37:37

tags:
  - nuxt
toc: true
categories:
  - - Frontend
    - vue
---

<article class="message is-info"><div class="message-body">
部落格原本使用的是 @nuxt/content 第二版，現在已經出到第三版了，這次的升級花了我整整三天。第一天升級後，出現大量錯誤，修了半天還是無法解決，受到心魔影響，看不太懂的錯誤訊息，最後只好整包 rollback 回到原點。後來重新閱讀文件，逐漸找到方向，最終花了兩天時間完成升級。本文章紀錄修改的過程，供有需要的人參考。

</div></article>

<!--more-->

## 目錄 | Contents

<div class="my-toc">
<!-- toc -->
</div>

---

## @nuxt/content v3

[Nuxt Content](https://content.nuxt.com/docs/getting-started/installation) 在 2025 年 1 月 16 日推出了 v3 版本，這次的更新專為 Nuxt 開發人員設計，並引入了基於 Git 的強大 CMS。

### 新功能

#### Content Collections

Collections 允許將專案內容分類，例如 `docs`、`blog` 等，使大型資料集的管理更加高效。

#### Improved Performance

v2 的一大挑戰是儲存檔案所需的捆綁包體積過大，特別影響無伺服器部署。v3 透過轉向 SQL 型存儲解決此問題，新的資料庫系統優化了數據結構，提高了效能與可擴展性。

#### TypeScript Integration

v3 強化了對 TypeScript 的支援，要求開發者更明確地定義內容結構。根據 Collections 定義，提供更嚴格的類型安全性，確保開發過程更穩定。

#### Nuxt Studio Integration（即將推出）

Studio 模組現已內建於 Nuxt Content，為開發者提供理想的開發環境，使開發者能專注於程式碼，而團隊成員則可透過直覺化介面管理內容。

## Content V2 升級至 V3 筆記

### 更新 @nuxt/content 版本

目前最新的安裝指令：

```sh
npm install @nuxt/content@3.1.0
```

更新 `package.json`：

```diff
"dependencies": {
- "@nuxt/content": "^2.13.4",
+ "@nuxt/content": "^3.1.0",
}
```

### 升級錯誤修正

升級後啟動時，可能會出現大量錯誤，主要來自已棄用的類型或方法，需要逐一修正：

- `NavItem` 全部移除，改為 `ContentNavigationItem`
- `.path` 仍保持 `.path`，但所有 `_` 前綴的內部欄位已重新命名，如 `._file` 改為 `.file`，`._dir` 改為 `.dir`
- `_dir.yml` 檔案改名為 `.navigation.yml`
- `content/index.yml` 改為 `content/index.md`，`content/blog.yml` 獨立定義

### 清理 `nuxt.config.ts` 設定

```diff
content: {
- navigation: {
- fields: ['description', 'publishedAt', 'isDirRoot', 'tags', 'image'],
},
},
```

### 新增 `content.config.ts`

```ts
import { defineContentConfig, defineCollection, z } from "@nuxt/content";

export default defineContentConfig({
  collections: {
    landing: defineCollection({
      type: "page",
      source: "index.md",
    }),
    blog: defineCollection({
      type: "page",
      source: {
        include: "**",
        exclude: ["index.md"],
      },
      schema: z.object({
        draft: z.boolean().default(false),
        description: z.string(),
        author: z.string(),
        publishedAt: z.string(),
        updated: z.string(),
        tags: z.string(),
        image: z.object({
          src: z.string(),
          alt: z.string(),
        }),
      }),
    }),
  },
});
```

### 修正 `queryContent`

```ts
const { data: page } = await useAsyncData(
  route.path,
  () =>
    Promise.all([
      queryCollection("blog").path(route.path).first(),
      queryCollectionItemSurroundings("blog", route.path, {
        fields: ["title", "description"],
      }),
    ]),
  {
    transform: ([page, surround]) => ({ page, surround }),
  }
);

if (!page.value) {
  throw createError({
    statusCode: 404,
    statusMessage: `path ${route.path}, Page not found`,
    fatal: true,
  });
}
```

### `app.vue` `fetchContentNavigation` 修改

```ts
const { data: navigation } = await useAsyncData("navigation", () =>
  queryCollectionNavigation("blog")
);
const { data: files } = useLazyAsyncData(
  "search",
  () => queryCollectionSearchSections("blog"),
  {
    server: false,
  }
);
```

### `ContentRenderer`

`mdcComponents` 不需額外定義，現在可自動匯入。

```diff
- <ContentRenderer :value="page" tag="article" :components="mdcComponents"> </ContentRenderer>
+ <ContentRenderer v-if="page" :value="page" :prose="false" />
```

### 刪除 `server/api/search`

刪除 `server/api/search.json.get.ts`，因 `/api/search.json` 已不再需要，否則可能導致錯誤。

### SQLite

升級成功後，應會生成以下檔案：

```
.data/content/contents.sqlite
```

該檔案無法直接開啟查看資料內容，需使用 SQLite 工具。

#### DB Browser for SQLite

前往 [下載 DB Browser for SQLite](https://sqlitebrowser.org/) 並安裝。

### `nuxt-og-image` 升級

`defineOgImageComponent` 無法找到，需升級至最新版本。

```sh
npm install nuxt-og-image@4.1.2
```

```js {2}
- "nuxt-og-image": "^2.2.4", // [!code focus]
+ "nuxt-og-image": "^4.1.2",
```

## 需要升級嗎？

老實說，這次升級似乎對小型專案影響不大，特別是文章數量不多時。不過，這次改動讓 TypeScript 和 schema 設定更加完善，未來擴充性更好。Content 自動匯入功能也相當便利！
