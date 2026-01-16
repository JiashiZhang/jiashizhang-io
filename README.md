# Jiashi Zhang | Personal Portfolio Website

![Jiashi Zhang | Personal Portfolio Website](public/social_img.webp)

[English](#english) | [中文](#chinese)

<a name="english"></a>
## English

This is my personal portfolio website built with Astro and TailwindCSS. It includes a blog, project showcase, CV, and more.

### Demo

View a live demo of [Jiashi Zhang](https://jiashizhang.io/)

### Installation

Run the following command in your terminal

```bash
npm install
```

Once the packages are installed you are ready to run astro. Astro comes with a built-in development server that has everything you need for project development. The astro dev command will start the local development server so that you can see your new website in action for the very first time.

```bash
npm run dev
```

### Tech Stack

- [Astro](https://astro.build)
- [tailwindcss](https://tailwindcss.com/)
- [DaisyUI](https://daisyui.com/)

### Project Structure

```php
├── src/
│   ├── components/
│   │   ├── cv/
│   │   │   ├── TimeLine
│   │   ├── BaseHead.astro
│   │   ├── Card.astro
│   │   ├── Footer.astro
│   │   ├── Header.astro
│   │   └── HorizontalCard.astro
│   │   └── SideBar.astro
│   │   └── SideBarMenu.astro
│   │   └── SideBarFooter.astro
│   ├── content/
│   │   ├── blog/
│   │   │   ├── post1.md
│   │   │   ├── post2.md
│   │   │   └── post3.md
│   │   ├── store/
│   │   │   ├── item1.md
│   │   │   ├── item2.md
│   ├── layouts/
│   │   └── BaseLayout.astro
│   │   └── PostLayout.astro
│   └── pages/
│   │   ├── blog/
│   │   │   ├── [...page].astro
│   │   │   ├── [slug].astro
│   │   └── cv.astro
│   │   └── index.astro
│   │   └── projects.astro
│   │   └── rss.xml.js
│   ├── styles/
│   │   └── global.css
│   └── config.ts
├── public/
│   ├── favicon.svg
│   └── profile.webp
│   └── social_img.webp
├── astro.config.mjs
├── tailwind.config.cjs
├── package.json
└── tsconfig.json
```

### Site config

You can change global site configuration on '/src/config.ts' file:

- **SITE_TITLE**: Default pages title.
- **SITE_DESCRIPTION**: Default pages title.
- **GENERATE_SLUG_FROM_TITLE**: By default Astrofy will generate the blog slug pages base on the article name. Set this var to false if you want to use the Astro file base (Compatible with Astrofy older versions).
- **TRANSITION_API**: Enable and disable transition API

### Components usage

#### Layout Components

The `BaseHead`, `Footer`, `Header`, and `SideBar` components are already included in the layout system. To change the website content you can edit the content of these components.

##### SideBar

In the Sidebar you can change your profilePicture, links to all your website pages, and your social icons.

You can change your avatar shape using [mask classes](https://daisyui.com/components/mask/).

The used social-icons are SVG form [BoxIcons](https://boxicons.com/) pack. You can replace the icons in the `SideBarFooter` component

To add a new page in the sidebar go to the `SideBarMenu` component.

```
<li><a class="py-3 text-base" id="home" href="/">Home</a></li>

```

**Note**: In order to change the sidebar menu's active item, you need to setup the prop `sideBarActiveItemID` in the `BaseLayout` component of your new page and add that id to the link in the `SideBarMenu`

#### TimeLine

The timeline components are used to confirm the CV.

```html
<div class="time-line-container">
  <TimeLineElement title="Element Title" subtitle="Subtitle">
    Content that can contain
    <div>divs</div>
    and <span>anything else you want</span>.
  </TimeLineElement>
  ...
</div>
```

#### Card & HorizontalCard

The cards are primarly used for the Project and the Blog components. They include a picture, a title, and a description. 

```html
<HorizontalCard title="Card Title" img="imge_url" desc="Description" url="Link
URL" target="Optional link target (_blank default)" badge="Optional badge"
tags={['Array','of','tags']} />
```

#### HorizontalCard Shop Item

This component is already included in the Store layout of the template. In case you want to use it in another place these are the props.

```html
<HorizontalShopItem
  title="Item Title"
  img="imge_url"
  desc="Item description"
  pricing="current_price"
  oldPricing="old_price"
  checkoutUrl="external store checkout url"
  badge="Optional badge"
  url="item details url"
  custom_link="Custom link url"
  custom_link_label="Cutom link btn label"
  target="Optional link target (_self default)"
/>
```

#### Adding a Custom Component

To add a custom component, you can create a .astro file in the components folder under the source folder. 

Components must follow this template. The ```---``` represents the code fence and uses Javascript and can be used for imports. 

The HTML component is the actual style of your new component. 

```html
---
// Component Script (JavaScript)
---
<!-- Component Template (HTML + JS Expressions) -->
```

For more details, see the [astro components](https://docs.astro.build/en/core-concepts/astro-components/) documentation here. 

### Layouts

Include `BaseLayout` in each page you add and `PostLayout` to your post pages.

The BaseLayout defines a general template for each new webpage you want to add. It imports constants SITE_TITLE and SITE_DESCRIPTION which can be modified in the ```../config``` folder. Data placed there can be imported anywhere using import. 

### Content

You can add a [content collection](https://docs.astro.build/en/guides/content-collections/) in `/content/' folder, you will need add it at config.ts.

#### config.ts

Where you need to define your content collections, we define our content schemas too.

#### Blog

Add your `md` blog post in the `/content/blog/` folder.

##### Post format

Add code with this format in the top of each post file.

```
---
title: "Post Title"
description: "Description"
pubDate: "Post date format(Sep 10 2022)"
heroImage: "Post Hero Image URL"
---
```

### Pages

#### Blog

Blog uses Astro's content collection to query post's `md`.

##### [page].astro

The `[page].astro` is the route to work with the paginated post list. You can change there the number of items listed for each page and the pagination button labels.

##### [slug].astro

The `[slug].astro` is the base route for every blog post, you can customize the page layout or behaviour, by default uses `content/blog` for content collection and `PostLayout` as layout.

#### Shop

Add your `md` item in the `/pages/shop/` folder.

##### [page].astro

The `[page].astro` is the route to work with the paginated item list. You can change there the number of items listed for each page and the pagination button labels. The shop will render all `.md` files you include inside this folder.

##### Item format

Add code with this format at the top of each item file.

```js
---
title: "Demo Item 1"
description: "Item description"
heroImage: "Item img url"
details: true // show or hide details btn
custom_link_label: "Custom btn link label"
custom_link: "Custom btn link"
pubDate: "Sep 15 2022"
pricing: "$15"
oldPricing: "$25.5"
badge: "Featured"
checkoutUrl: "https://checkouturl.com/"
---
```

#### Static pages

The other pages included in the template are static pages. The `index` page belongs to the root page. You can add your pages directly in the `/pages` folder and then add a link to those pages in the `sidebar` component.

Feel free to modify the content included in the pages that the template contains or add the ones you need.

### Theming

To change the template theme change the `data-theme` attribute of the `<html>` tag in `BaseLayout.astro` file.

You can choose among 30 themes available or create your custom theme. See themes available [here](https://daisyui.com/docs/themes/).

### Sitemap

The Sitemap is generated automatically when you build your website in the root of the domain. Please update the `robots.txt` file in the public folder with your site name URL for the Sitemap.

### Deploy

You can deploy your site on your favourite static hosting service such as Vercel, Netlify, GitHub Pages, etc.

The configuration for the deployment varies depending on the platform where you are going to do it. See the [official Astro information](https://docs.astro.build/en/guides/deploy/) to deploy your website.

> **⚠️ CAUTION** </br>
> The Blog pagination of this template is implemented using dynamic route parameters in its filename and for now this format is incompatible with SSR deploy configs, so please use the default static deploy options for your deployments.

### Contributing

Suggestions and pull requests are welcomed! Feel free to open a discussion or an issue for a new feature request or bug.

### License

This project is licensed under the MIT license.

<a name="chinese"></a>
## 中文

这是我使用 Astro 和 TailwindCSS 构建的个人作品集网站。它包括博客、项目展示、简历等功能。

### 演示

查看 [Jiashi Zhang](https://jiashizhang.io/) 的在线演示

### 安装

在终端中运行以下命令：

```bash
npm install
```

安装完成后，您就可以运行 Astro 了。Astro 自带一个内置的开发服务器，包含了项目开发所需的一切。`astro dev` 命令将启动本地开发服务器，这样您就可以第一时间看到您的新网站了。

```bash
npm run dev
```

### 技术栈

- [Astro](https://astro.build)
- [tailwindcss](https://tailwindcss.com/)
- [DaisyUI](https://daisyui.com/)

### 项目结构

```php
├── src/
│   ├── components/
│   │   ├── cv/
│   │   │   ├── TimeLine
│   │   ├── BaseHead.astro
│   │   ├── Card.astro
│   │   ├── Footer.astro
│   │   ├── Header.astro
│   │   └── HorizontalCard.astro
│   │   └── SideBar.astro
│   │   └── SideBarMenu.astro
│   │   └── SideBarFooter.astro
│   ├── content/
│   │   ├── blog/
│   │   │   ├── post1.md
│   │   │   ├── post2.md
│   │   │   └── post3.md
│   │   ├── store/
│   │   │   ├── item1.md
│   │   │   ├── item2.md
│   ├── layouts/
│   │   └── BaseLayout.astro
│   │   └── PostLayout.astro
│   └── pages/
│   │   ├── blog/
│   │   │   ├── [...page].astro
│   │   │   ├── [slug].astro
│   │   └── cv.astro
│   │   └── index.astro
│   │   └── projects.astro
│   │   └── rss.xml.js
│   ├── styles/
│   │   └── global.css
│   └── config.ts
├── public/
│   ├── favicon.svg
│   └── profile.webp
│   └── social_img.webp
├── astro.config.mjs
├── tailwind.config.cjs
├── package.json
└── tsconfig.json
```

### 网站配置

您可以在 `/src/config.ts` 文件中更改全局网站配置：

- **SITE_TITLE**: 默认页面标题。
- **SITE_DESCRIPTION**: 默认页面描述。
- **GENERATE_SLUG_FROM_TITLE**: 默认情况下，Astrofy 会根据文章名称生成博客 slug 页面。如果您想使用 Astro 文件基础（兼容 Astrofy 旧版本），请将此变量设置为 false。
- **TRANSITION_API**: 启用和禁用过渡 API。

### 组件使用

#### 布局组件

`BaseHead`、`Footer`、`Header` 和 `SideBar` 组件已包含在布局系统中。要更改网站内容，您可以编辑这些组件的内容。

##### 侧边栏 (SideBar)

在侧边栏中，您可以更改个人资料图片、所有网站页面的链接以及社交图标。

您可以使用 [mask classes](https://daisyui.com/components/mask/) 更改头像形状。

使用的社交图标来自 [BoxIcons](https://boxicons.com/) 包的 SVG。您可以在 `SideBarFooter` 组件中替换图标。

要在侧边栏中添加新页面，请转到 `SideBarMenu` 组件。

```
<li><a class="py-3 text-base" id="home" href="/">Home</a></li>

```

**注意**：为了更改侧边栏菜单的活动项，您需要在新页面的 `BaseLayout` 组件中设置 `sideBarActiveItemID` 属性，并将该 id 添加到 `SideBarMenu` 中的链接。

#### 时间轴 (TimeLine)

时间轴组件用于确认简历。

```html
<div class="time-line-container">
  <TimeLineElement title="Element Title" subtitle="Subtitle">
    Content that can contain
    <div>divs</div>
    and <span>anything else you want</span>.
  </TimeLineElement>
  ...
</div>
```

#### 卡片和水平卡片 (Card & HorizontalCard)

卡片主要用于项目和博客组件。它们包括图片、标题和描述。

```html
<HorizontalCard title="Card Title" img="imge_url" desc="Description" url="Link
URL" target="Optional link target (_blank default)" badge="Optional badge"
tags={['Array','of','tags']} />
```

#### 水平商店商品卡片 (HorizontalCard Shop Item)

此组件已包含在模板的商店布局中。如果您想在其他地方使用它，这些是属性。

```html
<HorizontalShopItem
  title="Item Title"
  img="imge_url"
  desc="Item description"
  pricing="current_price"
  oldPricing="old_price"
  checkoutUrl="external store checkout url"
  badge="Optional badge"
  url="item details url"
  custom_link="Custom link url"
  custom_link_label="Cutom link btn label"
  target="Optional link target (_self default)"
/>
```

#### 添加自定义组件

要添加自定义组件，您可以在源文件夹下的 components 文件夹中创建一个 .astro 文件。

组件必须遵循此模板。```---``` 代表代码栅栏，使用 Javascript，可用于导入。

HTML 组件是新组件的实际样式。

```html
---
// Component Script (JavaScript)
---
<!-- Component Template (HTML + JS Expressions) -->
```

有关更多详细信息，请参阅此处的 [astro components](https://docs.astro.build/en/core-concepts/astro-components/) 文档。

### 布局

在您添加的每个页面中包含 `BaseLayout`，并在您的文章页面中包含 `PostLayout`。

BaseLayout 为您想要添加的每个新网页定义了一个通用模板。它导入常量 SITE_TITLE 和 SITE_DESCRIPTION，可以在 ```../config``` 文件夹中修改。放置在那里的数据可以使用 import 在任何地方导入。

### 内容

您可以在 `/content/` 文件夹中添加 [content collection](https://docs.astro.build/en/guides/content-collections/)，您需要在 config.ts 中添加它。

#### config.ts

在这里您需要定义内容集合，我们也定义了内容模式。

#### 博客 (Blog)

将您的 `md` 博客文章添加到 `/content/blog/` 文件夹中。

##### 文章格式

在每个文章文件的顶部添加此格式的代码。

```
---
title: "Post Title"
description: "Description"
pubDate: "Post date format(Sep 10 2022)"
heroImage: "Post Hero Image URL"
---
```

### 页面

#### 博客

博客使用 Astro 的内容集合来查询文章的 `md`。

##### [page].astro

`[page].astro` 是处理分页文章列表的路由。您可以在那里更改每页列出的项目数和分页按钮标签。

##### [slug].astro

`[slug].astro` 是每篇博客文章的基本路由，您可以自定义页面布局或行为，默认情况下使用 `content/blog` 作为内容集合，使用 `PostLayout` 作为布局。

#### 商店 (Shop)

将您的 `md` 商品添加到 `/pages/shop/` 文件夹中。

##### [page].astro

`[page].astro` 是处理分页商品列表的路由。您可以在那里更改每页列出的项目数和分页按钮标签。商店将渲染您包含在此文件夹内的所有 `.md` 文件。

##### 商品格式

在每个商品文件的顶部添加此格式的代码。

```js
---
title: "Demo Item 1"
description: "Item description"
heroImage: "Item img url"
details: true // show or hide details btn
custom_link_label: "Custom btn link label"
custom_link: "Custom btn link"
pubDate: "Sep 15 2022"
pricing: "$15"
oldPricing: "$25.5"
badge: "Featured"
checkoutUrl: "https://checkouturl.com/"
---
```

#### 静态页面

模板中包含的其他页面是静态页面。`index` 页面属于根页面。您可以直接在 `/pages` 文件夹中添加页面，然后在 `sidebar` 组件中添加指向这些页面的链接。

随意修改模板包含的页面中的内容或添加您需要的内容。

### 主题

要更改模板主题，请更改 `BaseLayout.astro` 文件中 `<html>` 标签的 `data-theme` 属性。

您可以从 30 种可用主题中进行选择，或创建自定义主题。在此处查看可用主题 [here](https://daisyui.com/docs/themes/).

### 站点地图 (Sitemap)

当您在域的根目录构建网站时，会自动生成站点地图。请使用您的站点名称 URL 更新 public 文件夹中的 `robots.txt` 文件以获取站点地图。

### 部署

您可以将您的网站部署在您最喜欢的静态托管服务上，例如 Vercel、Netlify、GitHub Pages 等。

部署的配置因您要执行此操作的平台而异。请参阅 [Astro 官方信息](https://docs.astro.build/en/guides/deploy/) 以部署您的网站。

> **⚠️ 注意** </br>
> 此模板的博客分页是使用其文件名中的动态路由参数实现的，目前此格式与 SSR 部署配置不兼容，因此请使用默认的静态部署选项进行部署。

### 贡献

欢迎提出建议和拉取请求！随意打开讨论或问题以获取新功能请求或错误。

### 许可证

本项目采用 MIT 许可证。
