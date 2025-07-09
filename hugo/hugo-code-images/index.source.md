+++
title = "图像"
type = "chapter"
weight = 4
+++

## 图像资源 

要处理图像，您必须以页面资源、全局资源或远程资源的形式访问文件。

### 页面资源 

页面资源是页面束（page bundle）中的文件。页面束是一个具有根目录下的 `index.md` 或 `_index.md` 文件的目录。

```text
content/
└── posts/
    └── post-1/           <-- 页面束
        ├── index.md
        └── sunset.jpg    <-- 页面资源
```

要以页面资源的形式访问图像：

```go-html-template
{{ $image := .Resources.Get "sunset.jpg" }}
```

### 全局资源 

全局资源是位于 `assets` 目录中或装载到 `assets` 目录中任意目录中的文件。

```text
assets/
└── images/
    └── sunset.jpg    <-- 全局资源
```

要以全局资源的形式访问图像：

```go-html-template
{{ $image := resources.Get "images/sunset.jpg" }}
```

### 远程资源 

远程资源是可通过 HTTP 或 HTTPS 访问的远程服务器上的文件。要以远程资源的形式访问图像：

```go-html-template
{{ $image := resources.GetRemote "https://gohugo.io/img/hugo-logo.png" }}
```

## 图像渲染 

一旦您访问了页面资源或全局资源中的图像，可以在模板中使用 `Permalink`、`RelPermalink`、`Width` 和 `Height` 属性来渲染图像。

示例 1：如果未找到资源，则抛出错误。

```go-html-template
{{ $image := .Resources.GetMatch "sunset.jpg" }}
<img src="{{ $image.RelPermalink }}" width="{{ $image.Width }}" height="{{ $image.Height }}">
```

示例 2：如果未找到资源，则跳过图像渲染。

```go-html-template
{{ $image := .Resources.GetMatch "sunset.jpg" }}
{{ with $image }}
  <img src="{{ .RelPermalink }}" width="{{ .Width }}" height="{{ .Height }}">
{{ end }}
```

示例 3：另一种简洁的方式，如果未找到资源，则跳过图像渲染。

```go-html-template
{{ with .Resources.GetMatch "sunset.jpg" }}
  <img src="{{ .RelPermalink }}" width="{{ .Width }}" height="{{ .Height }}">
{{ end }}
```

示例 4：如果访问远程资源时遇到问题，则跳过渲染。

```go-html-template
{{ $u := "https://gohugo.io/img/hugo-logo.png" }}
{{ with resources.GetRemote $u }}
  {{ with .Err }}
    {{ errorf "%s" . }}
  {{ else }}
    <img src="{{ .RelPermalink }}" width="{{ .Width }}" height="{{ .Height }}">
  {{ end }}
{{ else }}
  {{ errorf "Unable to get remote resource %q" $u }}
{{ end }}
```

### `figure` 

`figure`是Markdown中图像语法的扩展，它没有提供更语义化的[HTML5 `<figure>` 元素][figureelement]的缩写。

`figure`短代码可以使用以下命名参数：

- src

  要显示图像的URL。

- link

  如果图像需要添加超链接，则为目标的URL。

- target

  如果设置了`link`参数，则为可选的`target`属性的URL。

- rel

  如果设置了`link`参数，则为可选的`rel`属性的URL。

- alt

  在图像无法显示时的替代文本。

- title

  图像标题。

- caption

  图像标题。`caption`值中的Markdown将被渲染。

- class

  HTML `figure`标签的`class`属性。

- height

  图像的`height`属性。

- width

  图像的`width`属性。

- loading

  图像的`loading`属性。

- attr

  图像属性文本。`attr`值中的Markdown将被渲染。

- attrlink

  如果属性文本需要超链接，请添加目标的URL。

#### `figure`输入示例 

figure-input-example.md
```go-html-template
{{< figure src="elephant.jpg" title="日落时的大象" >}}
```
