# Pandoc

Pandoc 是一个功能强大的文档格式转换软件。通过在命令行中输入简单的命令，即可将 Markdown、Word、HTML、PDF 等格式的文档进行相互转换。还可通过配置 CSS，让文档变得更美观。

## 安装

通过 [Pandoc 官网](https://www.pandoc.org/installing.html) 的教程安装即可。

## 文档

- [Pandoc - Demos](https://pandoc.org/demos.html)：这里列出了许多简单的示例。
- [Pandoc - Pandoc User's Guid](https://pandoc.org/MANUAL.html)：官方提供的详尽的使用文档。

## 示例

### 1. Markdown 转 Github 风格的 HTML

仅仅是 Markdown 转 HTML 的话很简单，只需下面这个命令即可。

````bash
pandoc input.md -o output.html
````

但这样生成的 HTML 文件看上去有些简陋，所以让我们找个 CSS 模板让它变得好看一些。

网上有很多现成的用于 Pandoc 的 CSS ，比如[这个](https://gist.github.com/forivall/7d5a304a8c3c809f0ba96884a7cf9d7e)。

将其下载到本地，通过下面这个命令就能让 Pandoc 套用模板了。

````bash
pandoc -c stylesheet.css --metadata pagetitle="My Output" --self-contained input.md -o output.html
````

其中：

- ``-c``：指定 CSS 文件的路径。
- ``--self-contained``：让 pandoc 把 CSS 的内容添加到新生成的 HTML 的头部中。注意：由于 Pandoc 套用 CSS 模板时，默认只会在新生成的 HTML 文件的头部加一个引用 CSS 文件的标签，所以如果不加 ``--self-contained`` 选项，改变两个文件的相对位置，模板的效果就会消失。
- ``--metadata``：可选项，为新生成的 HTML 文件添加一些信息。比如在此处就为新生成的 HTML 文件加了个 ``<title>`` 标签。

### 2. Markdown 转 Word 并套用一个模板

````bash
pandoc input.md -o output.docx --reference-doc=template.docx
````

其中：

- ``--reference-doc``：用于指定模板文件。
