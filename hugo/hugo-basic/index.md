# hugo目录结构

## 目录 

每个子目录都贡献于站点的内容、结构、行为或呈现。

- archetypes

  `archetypes` 目录包含用于新内容的模板。详见 [详情](https://hugo.opendocs.io/content-management/archetypes/).

- assets

  `assets` 目录包含通常通过资源管道传递的全局资源。包括图片、CSS、Sass、JavaScript 和 TypeScript 等资源。详见 [详情](https://hugo.opendocs.io/hugo-pipes/introduction/).

- config

  `config` 目录包含站点配置，可能分为多个子目录和文件。对于配置较少或不需要在不同环境中以不同方式运行的项目，项目根目录中的单个 `hugo.toml` 配置文件就足够了。详见 [详情](https://hugo.opendocs.io/getting-started/configuration/#configuration-directory)。

- content

  `content` 目录包含组成站点内容的标记文件（通常是 markdown）和页面资源。详见 [详情](https://hugo.opendocs.io/content-management/organization/).

- data

  `data` 目录包含用于增强内容、配置、本地化和导航的数据文件（JSON、TOML、YAML 或 XML）。详见 [详情](https://hugo.opendocs.io/templates/data-templates/).

- i18n

  `i18n` 目录包含多语言站点的翻译表。详见 [详情](https://hugo.opendocs.io/content-management/multilingual/).

- layouts

  `layouts` 目录包含将内容、数据和资源转换为完整网站的模板。详见 [详情](https://hugo.opendocs.io/templates/).

- public

  `public` 目录包含发布的网站，在运行 `hugo` 命令时生成。Hugo 根据需要重建此目录及其内容。详见 [详情](https://hugo.opendocs.io/getting-started/usage/#build-your-site).

- resources

  `resources` 目录包含 Hugo 资源管道的缓存输出，在运行 `hugo` 或 `hugo server` 命令时生成。默认情况下，此缓存目录包括 CSS 和图片。Hugo 根据需要重建此目录及其内容。

- static

  `static` 目录包含在构建站点时将复制到 public 目录的文件，例如 `favicon.ico`、`robots.txt` 和用于验证站点拥有权的文件。在引入 [页面包](https://hugo.opendocs.io/getting-started/glossary/#page-bundle) 和 [资源管道](https://hugo.opendocs.io/hugo-pipes/introduction/) 之前，`static` 目录也用于存放图片、CSS 和 JavaScript 等资源。详见 [详情](https://hugo.opendocs.io/content-management/static-files/).

- themes

  `themes` 目录包含一个或多个[主题](https://hugo.opendocs.io/getting-started/glossary/#theme)，每个主题位于自己的子目录中。

## 联合文件系统 

Hugo 创建了一个联合文件系统，允许将两个或多个目录挂载到同一位置。例如，假设您的主目录包含一个 Hugo 项目的目录，另一个目录包含共享内容：

```text
home/
└── user/
    ├── my-site/            
    │   ├── content/
    │   │   ├── books/
    │   │   │   ├── _index.md
    │   │   │   ├── book-1.md
    │   │   │   └── book-2.md
    │   │   └── _index.md
    │   ├── themes/
    │   │   └── my-theme/
    │   └── hugo.toml
    └── shared-content/     
        └── films/
            ├── _index.md
            ├── film-1.md
            └── film-2.md
```

您可以使用挂载（mounts）在构建站点时包含共享内容。在站点配置中：

hugo.

yamltomljson

```yaml
module:
  mounts:
  - source: content
    target: content
  - source: /home/user/shared-content
    target: content
```

当您在一个目录上覆盖另一个目录时，您必须挂载这两个目录。

如果您认为在项目目录中需要符号链接，请改用 Hugo 的联合文件系统。

挂载后，联合文件系统的结构如下：

```text
home/
└── user/
    └── my-site/
        ├── content/
        │   ├── books/
        │   │   ├── _index.md
        │   │   ├── book-1.md
        │   │   └── book-2.md
        │   ├── films/
        │   │   ├── _index.md
        │   │   ├── film-1.md
        │   │   └── film-2.md
        │   └── _index.md
        ├── themes/
        │   └── my-theme/
        └── hugo.toml
```
