.. highlightlang:: python

HTML主题支持
====================

.. versionadded:: 0.6

Sphinx可以通过主题来改变HTML输出的样式，主题是一个包括模板、样式表和静态文件
的集合。另外，主题还包括一个配置文件，通过这个配置文件可以指定主题、选择高亮
格式，同时还可以确定定制主题例如Logo等信息的选项。

主题意味着通用的，所以他们可以在不被改动的情况下用于不同的Sphinx项目。


使用主题
-------------

使用一个存在的主题是很容易的，如果选择使用Sphinx内置主题，那么你只需要配置
`html_theme`,通过配置 `html_theme_options` ,你可以更详细的配置主题。比如你
可以像下边的例子一样在你的 `conf.py` 中配置:: 

    html_theme = "default"
    html_theme_options = {
        "rightsidebar": "true",
        "relbarbgcolor": "black"
    }

以上配置将会用默认主题配置你的Sphinx文档，不一样的是，你的主题页面将会带着
一个右边栏，同时关系栏也将被设为黑色背景(关系栏就是在页眉和页脚带着导航连接
的栏)。

如果你选择的主题不是Sphinx内置主题，那么他必须是一个包含 `theme.conf` 文件的
文件夹或者zip压缩包，主题包需要被放在可以被Sphinx找到的地方，这个位置可以在
`html_theme_path` 被设置，这个值给了一个目录列表，每个目录包含 `conf.py` ，
包括主题目录或zip文件。例如，如果你有一个主题文件放在 `blue.zip` 里，你可以将
`blue.zip` 放到包含 `conf.py` 文件的目录里并使用以下配置::

    html_theme = "blue"
    html_theme_path = ["."]

如果你已经安装 ``setuptools`` 包，你可以使用第三种方法即向Sphinx提供主题的
地址。你需要在setup.py文件里的entry_points条目写入 ``sphinx_themes`` ，并
增加一个返回主题目录地址的 ``get_path`` 函数::

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

  - **nosidebar** (true 或 false): 不包括边栏.  默认是false.

  - **sidebarwidth** (一个 integer): 边栏的宽.  (以像素为单位，但是不要在参
  数中加入 ``px`` 值.)  默认宽为230像素.

* **default** -- 这是Sphinx的默认主题, 诸如 `the Python
  documentation <http://docs.python.org/>` 就是采用这个模板.  你可以通过以下
  选项定制主题:

  - **rightsidebar** (true 或 false): 将边栏放在右边，默认是false.

  - **stickysidebar** (true 或 false): 边栏固定，使边栏不随页面的滚动而滚
  动,它可能不兼容所有浏览器。默认是false。

  - **collapsiblesidebar** (true 或 false): 通过Javascript代码片段使边栏实
  现折叠，*不要和"rightsidebar" "stickysidebar"同时使用*，默认是false。

  - **externalrefs** (true 或 false): 内部连接和外部链接显示区别，默认是flase。

  这里还有一些颜色和字体选项可以方便的更改主题的配色，不用写样式表。

  - **footerbgcolor** (CSS color): 页脚(footer)的背景颜色。
  - **footertextcolor** (CSS color): 页脚(footer)的文本颜色.
  - **sidebarbgcolor** (CSS color): 边栏的背景颜色.
  - **sidebarbtncolor** (CSS color): 控制边栏折叠按钮的背景颜色
  (当 *collapsiblesidebar* 是 true 的时候使用).
  - **sidebartextcolor** (CSS color): 边栏的文本颜色.
  - **sidebarlinkcolor** (CSS color): 边栏的链接颜色.
  - **relbarbgcolor** (CSS color): 关系栏的背景颜色.
  - **relbartextcolor** (CSS color): 关系栏的文本颜色.
  - **relbarlinkcolor** (CSS color): 关系栏的链接颜色.
  - **bgcolor** (CSS color): 整体背景颜色.
  - **textcolor** (CSS color): 整体文本颜色.
  - **linkcolor** (CSS color): 整体链接颜色.
  - **visitedlinkcolor** (CSS color): 以访问过链接颜色.
  - **headbgcolor** (CSS color): 标题背景颜色.
  - **headtextcolor** (CSS color): 标题文本颜色.
  - **headlinkcolor** (CSS color): 标题链接颜色.
  - **codebgcolor** (CSS color): 代码块的背景颜色.
  - **codetextcolor** (CSS color): 代码块的默认文本颜色(如果没有配置高亮)。

  - **bodyfont** (CSS font-family): 正常文本的字体.
  - **headfont** (CSS font-family): 标题的字体.

* **sphinxdoc** -- 主要用于文档的模板，特点是右边栏。目前除了 *nosidebar* 
  和 *sidebarwidth*. 没有其他选项。

* **scrolls** -- 一个更轻量的主题，基于 `jinja的文档主题 <http://jinja.pocoo.org/>` 。下面的颜色选项是可配置的:

  - **headerbordercolor**
  - **subheadlinecolor**
  - **linkcolor**
  - **visitedlinkcolor**
  - **admonitioncolor**

* **agogo** -- Andi Albrecht创作的一个主题.支持下列选项:

  - **bodyfont** (CSS font family): 正常文本的字体.
  - **headerfont** (CSS font family): 标题字体.
  - **pagewidth** (CSS length): 页面内容的宽度, 默认为70em.
  - **documentwidth** (CSS length): 文档的宽度 (不带边栏),
    默认为50em.
  - **sidebarwidth** (CSS length): 边栏的宽度, 默认为20em.
  - **bgcolor** (CSS color): 背景颜色.
  - **headerbg** (CSS value for "background"): 标题部分的背景颜色，默认
  为渐变浅灰  .
  - **footerbg** (CSS value for "background"): 页脚部分的背景颜色，默认
  为渐变浅灰  .
  - **linkcolor** (CSS color): 整体链接颜色.
  - **headercolor1**, **headercolor2** (CSS color): <h1>标题和<h2>标题
  的背景颜色，默认为渐变浅灰。
  - **headerlinkcolor** (CSS color): 题目中反向引用链接的颜色.
  - **textalign** (CSS *text-align* value): 整体的文本对齐方式，默认为 
  ``justify`` .

* **nature** -- 一个绿色色调主题.目前除了 *nosidebar* 和 *sidebarwidth* 
没有其他配置选项。

* **pyramid** -- 来自Pyramid框架的一个主题，设计者是Blaise Laflamme. 目
前除了 *nosidebar* 和 *sidebarwidth* 没有其他配置选项。

* **haiku** -- 一个没有边栏的主题，灵感来自 `Haiku OS user guide
  <http://www.haiku-os.org/docs/userguide/en/contents.html>`_.支持以下
  选项:

  - **full_logo** (true 或 false, 默认为false): 如果选择true,头部将只会
  显示:confval:`html_logo`.  Use this for large logos.如果设置为false, 
  logo (如果存在)将会浮动在右边,文档标题将会显示在头部。
  - **textcolor**, **headingcolor**, **linkcolor**, **visitedlinkcolor**,
    **hoverlinkcolor** (CSS colors): 各种Body元素的颜色.

* **traditional** -- 类似以前python文档的主题.目前除了 *nosidebar* 和 *sidebarwidth* 没有其他选项.

* **epub** -- 一个用于编译epub的主题. 这个主题尽力节省视觉空间,是哥ebook的稀缺资
源。支持以下选项:

  - **relbar1** (true 或 false,默认为true): 如果选择true,将会生成 `relbar1`
  ,否则省略。
  - **footer**  (true 或 false,默认为true): 如果选择true,将会生成 `footer`,
  否则省略。

创建主题
---------------

As said, themes are either a directory or a zipfile (whose name is the theme
name), containing the following:

* A :file:`theme.conf` file, see below.
* HTML templates, if needed.
* A ``static/`` directory containing any static files that will be copied to the
  output static directory on build.  These can be images, styles, script files.

The :file:`theme.conf` file is in INI format [1]_ (readable by the standard
Python :mod:`ConfigParser` module) and has the following structure:

.. sourcecode:: ini

    [theme]
    inherit = base theme
    stylesheet = main CSS name
    pygments_style = stylename

    [options]
    variable = default value

* The **inherit** setting gives the name of a "base theme", or ``none``.  The
  base theme will be used to locate missing templates (most themes will not have
  to supply most templates if they use ``basic`` as the base theme), its options
  will be inherited, and all of its static files will be used as well.

* The **stylesheet** setting gives the name of a CSS file which will be
  referenced in the HTML header.  If you need more than one CSS file, either
  include one from the other via CSS' ``@import``, or use a custom HTML template
  that adds ``<link rel="stylesheet">`` tags as necessary.  Setting the
  :confval:`html_style` config value will override this setting.

* The **pygments_style** setting gives the name of a Pygments style to use for
  highlighting.  This can be overridden by the user in the
  :confval:`pygments_style` config value.

* The **options** section contains pairs of variable names and default values.
  These options can be overridden by the user in :confval:`html_theme_options`
  and are accessible from all templates as ``theme_<name>``.


Templating
~~~~~~~~~~

The :doc:`guide to templating <templating>` is helpful if you want to write your
own templates.  What is important to keep in mind is the order in which Sphinx
searches for templates:

* First, in the user's ``templates_path`` directories.
* Then, in the selected theme.
* Then, in its base theme, its base's base theme, etc.

When extending a template in the base theme with the same name, use the theme
name as an explicit directory: ``{% extends "basic/layout.html" %}``.  From a
user ``templates_path`` template, you can still use the "exclamation mark"
syntax as described in the templating document.


Static templates
~~~~~~~~~~~~~~~~

Since theme options are meant for the user to configure a theme more easily,
without having to write a custom stylesheet, it is necessary to be able to
template static files as well as HTML files.  Therefore, Sphinx supports
so-called "static templates", like this:

If the name of a file in the ``static/`` directory of a theme (or in the user's
static path, for that matter) ends with ``_t``, it will be processed by the
template engine.  The ``_t`` will be left from the final file name.  For
example, the *default* theme has a file ``static/default.css_t`` which uses
templating to put the color options into the stylesheet.  When a documentation
is built with the default theme, the output directory will contain a
``_static/default.css`` file where all template tags have been processed.


.. [1] It is not an executable Python file, as opposed to :file:`conf.py`,
       because that would pose an unnecessary security risk if themes are
       shared.

