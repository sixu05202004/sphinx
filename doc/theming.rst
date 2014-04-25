.. highlightlang:: python

HTML主题支持
====================

.. versionadded:: 0.6

Sphinx可以通过主题来改变HTML输出的样式，主题是一个包括模板、样式表和静态文件
的集合。另外，主题还包括一个配置文件，通过这个配置文件可以指定主题、选择高亮
格式，以及定制主题的例如Logo等信息等。

主题意味着项目无关的，所以他们对于Sphinx项目应该是通用的。


使用主题
-------------

使用一个存在的主题是很容易的，如果选择使用Sphinx内置主题，那么你只需要设置
:confval:`html_theme` 。此外，通过配置 :confval:`html_theme_options` ,你可
以更详细的配置主题。比如你可以像下边的例子一样在你的 :file:`conf.py` 中配置:: 

    html_theme = "default"
    html_theme_options = {
        "rightsidebar": "true",
        "relbarbgcolor": "black"
    }

以上配置将会使用默认主题来构建你的Sphinx项目，一点小区别是你的主题页面将会
带着一个右边栏，同时关系栏也将被设为黑色背景(关系栏就是在页眉和页脚带着导航
连接的栏)。

如果你选择的主题不是Sphinx内置主题，那么他必须是一个包含 :file:`theme.conf`
文件的文件夹或者zip压缩包，主题包需要被放在可以被Sphinx找到的地方，这个位置
可以在:confval:`html_theme_path` 被设置，但是需要和:file:`conf.py` 位于同级
目录下。例如，如果你有一个主题文件放在:file:`blue.zip` 里，你可以将:file:`blue.zip` 
放到包含 :file:`conf.py` 文件
的同级目录里并使用以下配置::

    html_theme = "blue"
    html_theme_path = ["."]

如果你已经安装 ``setuptools`` 包，你可以使用第三种方法即动态向Sphinx提供主
题的地址。你需要在setup.py文件里的entry_points条目写入 ``sphinx_themes`` ，
并增加一个返回主题目录地址的 ``get_path`` 函数::

    // in your 'setup.py'

    setup(
        ...
        entry_points = {
            'sphinx_themes': [
                'path = your_package:get_path',
            ]
        },
        ...
    )

    // in 'your_package.py'

    from os import path
    package_dir = path.abspath(path.dirname(__file__))
    template_path = path.join(package_dir, 'themes')

    def get_path():
        return  template_path 

.. versionadded:: 1.2
   'sphinx_themes' entry_points feature.


.. _builtin-themes:

内置主题
--------------

.. cssclass:: right

+--------------------+--------------------+
| **Theme overview** |                    |
+--------------------+--------------------+
| |default|          | |sphinxdoc|        |
|                    |                    |
| *default*          | *sphinxdoc*        |
+--------------------+--------------------+
| |scrolls|          | |agogo|            |
|                    |                    |
| *scrolls*          | *agogo*            |
+--------------------+--------------------+
| |traditional|      | |nature|           |
|                    |                    |
| *traditional*      | *nature*           |
+--------------------+--------------------+
| |haiku|            | |pyramid|          |
|                    |                    |
| *haiku*            | *pyramid*          |
+--------------------+--------------------+

.. |default|     image:: themes/default.png
.. |sphinxdoc|   image:: themes/sphinxdoc.png
.. |scrolls|     image:: themes/scrolls.png
.. |agogo|       image:: themes/agogo.png
.. |traditional| image:: themes/traditional.png
.. |nature|      image:: themes/nature.png
.. |haiku|       image:: themes/haiku.png
.. |pyramid|     image:: themes/pyramid.png

Sphinx内置了一些主题可供选择

内置主题如下:

* **basic** -- 这是一个被用于其他主题的无样式布局，也可以作为自定义定制主题
  的基础。HTML包含了所有重要的元素，比如边栏，关系栏等。这里有一些被其他主
  题继承的选项:

  - **nosidebar** (true 或 false): 不包括边栏，默认是false。

  - **sidebarwidth** (一个 integer): 边栏的宽，(以像素为单位，但是不要在参
  数中加入 ``px`` 值)  默认宽为230像素。

* **default** -- 这是Sphinx的默认主题, 诸如 `the Pythondocumentation <http://docs.python.org/>` 
就是采用这个模板。你可以通过以下选项定制主题:

  - **rightsidebar** (true 或 false): 将边栏放在右边，默认是false。

  - **stickysidebar** (true 或 false): 边栏固定，使边栏不随页面的滚动而滚
  动,它可能不兼容所有浏览器。默认是false。

  - **collapsiblesidebar** (true 或 false): 通过Javascript代码片段使边栏实
  现折叠，*不要和"rightsidebar" "stickysidebar"同时使用*，默认是false。

  - **externalrefs** (true 或 false): 内部连接和外部链接显示区别，默认是flase。

  这里还有一些颜色和字体选项可以方便的更改主题的配色，不用写样式表。

  - **footerbgcolor** (CSS color): 页脚(footer)的背景颜色。
  - **footertextcolor** (CSS color): 页脚(footer)的文本颜色。
  - **sidebarbgcolor** (CSS color): 边栏的背景颜色。
  - **sidebarbtncolor** (CSS color): 控制边栏折叠按钮的背景颜色。
  (当 *collapsiblesidebar* 是 true 的时候使用)。
  - **sidebartextcolor** (CSS color): 边栏的文本颜色。
  - **sidebarlinkcolor** (CSS color): 边栏的链接颜色。
  - **relbarbgcolor** (CSS color): 关系栏的背景颜色。
  - **relbartextcolor** (CSS color): 关系栏的文本颜色。
  - **relbarlinkcolor** (CSS color): 关系栏的链接颜色。
  - **bgcolor** (CSS color): Body背景颜色。
  - **textcolor** (CSS color): Body文本颜色。
  - **linkcolor** (CSS color): Body链接颜色。
  - **visitedlinkcolor** (CSS color): 已访问过链接颜色。
  - **headbgcolor** (CSS color): 标题背景颜色。
  - **headtextcolor** (CSS color): 标题文本颜色。
  - **headlinkcolor** (CSS color): 标题链接颜色。
  - **codebgcolor** (CSS color): 代码块的背景颜色。
  - **codetextcolor** (CSS color): 代码块的默认文本颜色(如果没有配置高亮)。

  - **bodyfont** (CSS font-family): 正常文本的字体。
  - **headfont** (CSS font-family): 标题的字体。

* **sphinxdoc** -- 主要用于文档的模板，特点是右边栏。目前除了 *nosidebar* 
  和 *sidebarwidth* 没有其他选项。

* **scrolls** -- 一个更轻量的主题，基于 `jinja的文档主题 <http://jinja.pocoo.org/>` 。下面的颜色选项是可配置的:

  - **headerbordercolor**
  - **subheadlinecolor**
  - **linkcolor**
  - **visitedlinkcolor**
  - **admonitioncolor**

* **agogo** -- Andi Albrecht创作的一个主题.支持下列选项:

  - **bodyfont** (CSS font family): 正常文本的字体。
  - **headerfont** (CSS font family): 标题字体。
  - **pagewidth** (CSS length): 页面内容的宽度, 默认为70em。
  - **documentwidth** (CSS length): 文档的宽度 (不带边栏),默认为50em。
  - **sidebarwidth** (CSS length): 边栏的宽度, 默认为20em。
  - **bgcolor** (CSS color): 背景颜色。
  - **headerbg** (CSS value for "background"): 标题部分的背景颜色，默认
  为渐变浅灰。
  - **footerbg** (CSS value for "background"): 页脚部分的背景颜色，默认
  为渐变浅灰。
  - **linkcolor** (CSS color): 整体链接颜色。
  - **headercolor1**, **headercolor2** (CSS color): <h1>标题和<h2>标题
  的背景颜色，默认为渐变浅灰。
  - **headerlinkcolor** (CSS color): 题目中反向引用链接的颜色。
  - **textalign** (CSS *text-align* value): 整体的文本对齐方式，默认为 
  ``justify`` 。

* **nature** -- 一个绿色色调主题。目前除了 *nosidebar* 和 *sidebarwidth* 
没有其他配置选项。

* **pyramid** -- 来自Pyramid框架项目的一个主题，设计者是Blaise Laflamme。
目前除了 *nosidebar* 和 *sidebarwidth* 没有其他配置选项。

* **haiku** -- 一个没有边栏的主题，灵感来自 `Haiku OS user guide
  <http://www.haiku-os.org/docs/userguide/en/contents.html>`_ 。支持以下
  选项:

  - **full_logo** (true 或 false, 默认为false): 如果选择true，头部将只会
  显示:confval:`html_logo` 。通过这个选项可以设置大Logo。如果设置为false， 
  logo (如果存在)将会浮动在右边，文档标题将会显示在头部。
  - **textcolor**, **headingcolor**, **linkcolor**, **visitedlinkcolor**,
    **hoverlinkcolor** (CSS colors): 各种Body元素的颜色。

* **traditional** -- 类似以前python文档的主题。目前除了 *nosidebar* 和
*sidebarwidth* 没有其他选项。

* **epub** -- 一个用于编译epub的主题. 这个主题尽力节省视觉空间,是ebook阅读
器的稀缺资源。支持以下选项:

  - **relbar1** (true 或 false,默认为true): 如果选择true，将会生成 `relbar1`
  ,否则省略。
  - **footer**  (true 或 false,默认为true): 如果选择true，将会生成 `footer`,
  否则省略。

创建主题
---------------

如上文所说，主题是一个文件夹或zip文件(名字就是主题名),包含以下内容:

* 一个:file:`theme.conf` 文件。
* HTML模板(如果需要)
* 一个包含静态文件的 ``static/``  文件夹，他将会被复制到构建目录的静
  态文件夹。静态文件包括图片、样式表、脚本文件等。

:file:`theme.conf` 文件应该是INI格式 [1]_ (可被python标准库的:mod:`ConfigParser`
模块识别)，他的结构如下:

.. sourcecode:: ini

    [theme]
    inherit = base theme
    stylesheet = main CSS name
    pygments_style = stylename

    [options]
    variable = default value

* **inherit** 可以设置为设置为 ``base theme`` 或 ``none`` 。base thmee
  将会被用于搜寻的主题(如果选择 ``basic`` 作为基本主题，那么不必不得不
  支持所有模板),他的选项将会被继承，它的静态文件也会被使用。

* **stylesheet** 设置了一个将会被在HTML头部引用的CSS文件，如果你需要更多
  的CSS文件, 可以通过CSS ``@import`` 引用其他CSS文件，或者使用一个定制的
  有 ``<link rel="stylesheet">`` 标签的HTML模板。如果设置 :confval:`html_style`
  将会覆盖这里的配置。

* **pygments_style** 设置Pygments风格来使用高亮。他会被:confval:`pygments_style`
  的配置覆盖。

* **options** 可以设置变量和及其对应值。这些选项会被:confval:`html_theme_options`
  的配置所覆盖。


模板
~~~~~~~~~~

:doc:`guide to templating <templating>` 可以帮助你写自己的模板。你需要特别
注意模板关于sphinx搜索的那块内容:

* 首先, 设置用户的 ``templates_path`` 的文件夹。
* 然后，选择主题。
* 最后，设置继承主题等等.

如果用一个相同的名字在base theme主题上进行扩展,你应该使用一个比较详细的目录:
``{% extends "basic/layout.html" %}`` 。在用户的 ``templates_path`` 模板。
你仍然可以使用 `exclamation mark`` 语法作为模板文档的描述。


静态模板
~~~~~~~~~~~~~~~

由于模板选项可以使用户很简单的定制自己的模板，而不用写样式表，因此我们称Sphinx
支持"静态模板"。

如果位于 ``static/`` 目录的主题的文件名字以 ``_t`` 结尾，那么他将会被模板
引擎解析, ``_`` 将会被留下。比如， *default* 主题有一个 ``static/default.css_t`` 
文件，当文档用默认主题构建时，会输出 ``_static/default.css`` 。

.. [1] :file:`conf.py`不应该是一个可执行的python文件，因为当主题分享的时候
   这将会事一个不必要的安全风险。
