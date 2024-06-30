Getting Started
=================
Sphinx 是一个文档生成器或一个工具，可将一组纯文本源文件转换为各种输出格式，自动生成交叉引用、索引等。也就是说，如果您有一个包含一堆 reStructuredText 或 Markdown 文档的目录，Sphinx可以生成一系列 HTML 文件、PDF 文件（通过 LaTeX）、手册页等等。

Sphinx 专注于文档，特别是手写文档，但是，Sphinx 也可用于生成博客、主页甚至书籍。 Sphinx 的强大功能很大程度上来自于其默认纯文本标记格式 reStructuredText 的丰富性及其显着的可扩展性功能。

本文档的目的是让您快速了解 Sphinx 是什么以及如何使用它。完成后，您可以查看安装指南，然后查看 Sphinx 使用的默认标记格式 reStructuredText 的介绍。

Setting up the documentation sources
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Sphinx 纯文本文档源集合的根目录称为源目录。该目录还包含 Sphinx 配置文件 conf.py，您可以在其中配置 Sphinx 如何读取源代码和构建文档的各个方面。 [1]

Sphinx 附带了一个名为 sphinx-quickstart 的脚本，该脚本设置源目录并创建默认的 conf.py，其中包含它询问您的几个问题中最有用的配置值。要使用它，请运行：
```
$ sphinx-quickstart
```

Defining document structure
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
假设您已经运行 sphinx-quickstart。它创建了一个包含conf.py 的源目录和一个根文档index.rst。根文档的主要功能是充当欢迎页面，并包含“目录树”（或目录树）的根。这是 Sphinx 添加到 reStructuredText 的主要内容之一，reStructuredText 是一种将多个文件连接到单个文档层次结构的方法。

reStructuredText directives
*****************************
toctree 是一个 reStructuredText 指令，一个非常通用的标记。指令可以有参数、选项和内容。
参数直接在指令名称后面的双冒号之后给出。每个指令决定它是否可以有参数以及有多少参数。
选项在参数之后以“字段列表”的形式给出。 maxdepth 就是 toctree 指令的一个选项。
内容跟在选项或参数的空行之后。每个指令决定是否允许内容以及如何处理它。
指令的一个常见问题是内容的第一行必须缩进到与选项相同的级别。

Adding content
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
在Sphinx源文件中，您可以使用标准reStructuredText的大部分功能。 Sphinx 还添加了一些功能。例如，您可以使用 ref 角色以可移植的方式添加跨文件引用（适用于所有输出类型）。

例如，如果您正在查看 HTML 版本，则可以查看此文档的源代码 - 使用侧边栏中的“显示源代码”链接。

Running the build
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
现在您已经添加了一些文件和内容，让我们对文档进行第一个构建。使用 sphinx-build 程序启动构建：
...
然而，sphinx-quickstart 脚本会创建一个 Makefile 和一个 make.bat，这使您的生活变得更加轻松。这些可以通过使用构建器的名称运行 make 来执行。例如。
```
$ make html
```
这将在您选择的构建目录中构建 HTML 文档。不带参数执行 make 以查看哪些目标可用。


Documenting Objects
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Sphinx 的主要目标之一是轻松记录任何域中的对象（在非常一般的意义上）。域是归于一类的对象类型的集合，包含用于创建和引用这些对象的描述的标记。

最突出的领域是 Python 域。例如，要记录 Python 的内置函数 enumerate()，您可以将下面这个添加到源文件之一:
...





.. py:function:: enumerate(sequence[, start=0])
   
   Return an iterator that yields tuples of an index and an item of the
   *sequence*. (And so on.)

.. function:: enumerate(sequence[, start=0])
   
   Return an iterator that yields tuples of an index and an item of the
   *sequence*. (And so on.)


The :py:func:`enumerate` function can be used for ...

The :func:`enumerate` function can be used for ...

Basic configuration
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
前面我们提到conf.py 文件控制Sphinx 如何处理您的文档。在作为 Python 源文件执行的该文件中，您可以分配配置值。对于高级用户：由于它是由 Sphinx 执行的，因此您可以在其中执行一些重要的任务，例如扩展 sys.path 或导入模块以查找您正在记录的版本。

您可能想要更改的配置值已由 sphinx-quickstart 放入 conf.py 中，并最初被注释掉（使用标准 Python 语法：# 注释该行的其余部分）。要更改默认值，请删除井号并修改该值。要自定义 sphinx-quickstart 不会自动添加的配置值，只需添加额外的分配即可。

请记住，该文件对字符串、数字、列表等使用 Python 语法。文件默认以 UTF-8 保存，如第一行的编码声明所示。

Autodoc
~~~~~~~~~~~
在编写 Python 代码时，通常会将大量文档以文档字符串的形式放在源文件中。 Sphinx 支持通过名为 autodoc 的扩展（扩展是为 Sphinx 项目提供附加功能的 Python 模块）包含模块中的文档字符串。

Intersphinx
~~~~~~~~~~~
许多 Sphinx 文档（包括 Python 官方文档）都发布在 Internet 上。当您想要从自己的文档中链接到此类文档时，可以使用 sphinx.ext.intersphinx 来完成。

为了使用 intersphinx，您需要在 conf.py 中激活它，方法是将字符串“sphinx.ext.intersphinx”放入 extensions 列表中，并设置 intersphinx_mapping 配置值。

For example, to link to io.open() in the Python library manual, you need to setup your intersphinx_mapping like:
```
intersphinx_mapping = {'python': ('https://docs.python.org/3', None)}
```

现在，您可以编写一个交叉引用，例如 :py:func:`io.open`。当前文档集中没有匹配目标的任何交叉引用都将在 intersphinx_mapping 中配置的文档集中查找（为下载有效目标列表，需要能访问该 URL）。 Intersphinx 还适用于其他一些域角色，包括 :ref:，但它不适用于 :doc:，因为这是非域角色。


More topics to be covered
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~