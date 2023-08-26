<h1 align="center">
    <img alt="cookiecutter Logo" width="200px" src="https://raw.githubusercontent.com/cookiecutter/cookiecutter/3ac078356adf5a1a72042dfe72ebfa4a9cd5ef38/logo/cookiecutter_medium.png">
</h1>

<div align="center">

[![pypi](https://img.shields.io/pypi/v/cookiecutter.svg)](https://pypi.org/project/cookiecutter/)
[![python](https://img.shields.io/pypi/pyversions/cookiecutter.svg)](https://pypi.org/project/cookiecutter/)
[![Build Status](https://github.com/cookiecutter/cookiecutter/actions/workflows/tests.yml/badge.svg?branch=master)](https://github.com/cookiecutter/cookiecutter/actions)
[![codecov](https://codecov.io/gh/cookiecutter/cookiecutter/branch/master/graphs/badge.svg?branch=master)](https://codecov.io/github/cookiecutter/cookiecutter?branch=master)
[![discord](https://img.shields.io/badge/Discord-cookiecutter-5865F2?style=flat&logo=discord&logoColor=white)](https://discord.gg/9BrxzPKuEW)
[![docs](https://readthedocs.org/projects/cookiecutter/badge/?version=latest)](https://readthedocs.org/projects/cookiecutter/?badge=latest)
[![Code Quality](https://img.shields.io/scrutinizer/g/cookiecutter/cookiecutter.svg)](https://scrutinizer-ci.com/g/cookiecutter/cookiecutter/?branch=master)

</div>

# cookiecutter-中英文对照文档
(本库主要是进行中文文档翻译学习，部分翻译内容是根据自己的理解翻译，非原句原样翻译。因译者水平有限，欢迎指正)

**cookiecutters**是一个帮助用户从项目模板中快速创建项目的命令行工具程序。例如，根据Python package工程模板快速创建一个Python package项目。

- Documentation: [https://cookiecutter.readthedocs.io](https://cookiecutter.readthedocs.io)
- GitHub: [https://github.com/cookiecutter/cookiecutter](https://github.com/cookiecutter/cookiecutter)
- PyPI: [https://pypi.org/project/cookiecutter/](https://pypi.org/project/cookiecutter/)
- Free and open source software: [BSD license](https://github.com/cookiecutter/cookiecutter/blob/main/LICENSE)


## Features
## 特点

- 跨平台:官方支持Windows，Mac，Linux
- 使用Cookiecutter的用户无需掌握或者编写Python代码
- 支持的Python版本包括:3.7, 3.8, 3.9, 3.10, 3.11
- 项目模板可以是任何编程语言或者标记文本格式:
  Python, JavaScript, Ruby, CoffeeScript, RST, Markdown, CSS, HTML 等编程语言或者标记文本格式.
  你可以在同一个项目模板中使用多种语言。

### 已经存在的用户可用模板

- 简单的命令行用法

  ```bash
  # Create project from the cookiecutter-pypackage.git repo template
  # You'll be prompted to enter values.
  # Then it'll create your Python package in the current working directory,
  # based on those values.
  $ cookiecutter https://github.com/audreyfeldroy/cookiecutter-pypackage
  # For the sake of brevity, repos on GitHub can just use the 'gh' prefix
  $ cookiecutter gh:audreyfeldroy/cookiecutter-pypackage
  ```

- 在命令行中通过本地模板创建项目

  ```bash
  # 在本地，创建项目在当前工作目录中的示例
  # cookiecutter-pypackage/ 表示模板目录
  $ cookiecutter cookiecutter-pypackage/
  ```

- 或者在Python中使用

  ```py
  from cookiecutter.main import cookiecutter

  # 通过本地目录cookiecutter-pypackage/中的模板来创建项目
  cookiecutter('cookiecutter-pypackage/')

  # 通过远程仓库中的cookiecutter-pypackage.git模板来创建项目
  cookiecutter('https://github.com/audreyfeldroy/cookiecutter-pypackage.git')
  ```

- 当你没有显式地使用`--no-input`时，系统会提示你输入:
  - 交互命令中的提示的输入变量是`cookiecutter.json`文件中keys
  - 默认的响应是`cookiecutter.json`文件中对应的value
  - 提示词的顺序是和`cookiecutter.json`文件中对应的顺序一致
    
- 跨平台支持 `~/.cookiecutterrc` 文件:

  ```yaml
  default_context:
    full_name: "Audrey Roy Greenfeld"
    email: "audreyr@gmail.com"
    github_username: "audreyfeldroy"
  cookiecutters_dir: "~/.cookiecutters/"
  ```

- Cookiecutters（克隆Cookiecutter工程模板）会默认将代码放入到`~/.cookiecutters/`目录或者指定的目录
- 如果你已经克隆了一个cookiecutter项目到`~/.cookiecutters/`目录，你可以通过目录名引用它:

  ```bash
  # Clone cookiecutter-pypackage
  $ cookiecutter gh:audreyfeldroy/cookiecutter-pypackage
  # Now you can use the already cloned cookiecutter by name
  $ cookiecutter cookiecutter-pypackage
  ```

- 你可以使用本地的cookiecutters模板或者远程仓库的cookiecutters模板
- 默认上下文:在生成工程时指定默认的key/value键值对
- 使用命令行参数注入默认的上下文参数:

  ```bash
  cookiecutter --no-input gh:msabramo/cookiecutter-supervisor program_name=foobar startsecs=10
  ```

- 直接访问Cookiecutter API时，允许注入额外的上下文参数
- 本地项目的路径可以被指定为绝对的或者相对的
默认生成的项目会在你的当前路径，或者通过`-o`制定目标路径。

### 面向模板开发者

- 支持无限制的目录嵌套层级
- 所有的目标均使用Jinja2开发完成。
- 目录名称和文件名称均可以支持模板化
  例如:

  ```py
  {{cookiecutter.repo_name}}/{{cookiecutter.repo_name}}/{{cookiecutter.repo_name}}.py
  ```
- 只需要在`cookiecutter.json` 文件中定义模板变量. 你可以通过`__prompts__`给每个变量增加用户可读性强的提示信息. Those human-readable questions supports [`rich` markup](https://rich.readthedocs.io/en/stable/markup.html) such as `[bold yellow]this is bold and yellow[/]`
  例如:

  ```json
  {
    "full_name": "Audrey Roy Greenfeld",
    "email": "audreyr@gmail.com",
    "project_name": "Complexity",
    "repo_name": "complexity",
    "project_short_description": "Refreshingly simple static site generator.",
    "release_date": "2013-07-10",
    "year": "2013",
    "version": "0.1.1",
    "linting": ["ruff", "flake8", "none"],
    "__prompts__": {
      "full_name": "Provide your [bold yellow]full name[/]",
      "email": "Provide your [bold yellow]email[/]",
      "linting": {
        "__prompt__": "Which [bold yellow]linting tool[/] do you want to use?",
        "ruff": "Ruff",
        "flake8": "Flake8",
        "none": "No linting tool"
      }
    }
  }
  ```
- 在生成项目前或者生成项目后调用的hooks:在项目生成前后运行的Python或Shell脚本。

## 可用的Cookiecutters

开发出好的项目需要许多cookiecutters模板和贡献者。
我们非常高兴有许多Cookiecutter项目模板可供选择。
我们希望你可以找到你需要的Cookiecutter项目模板。


### 一个丰富的Cookiecutters模板库

[Github search](https://github.com/search?q=cookiecutter&type=Repositories)是查找现成的Cookiecutters模板库最好的地方，执行在搜索框输入`cookiecutter`，就可以找到超过4000个相关的资源库。

我们也建议你检查相关GitHub主题，常用的有[cookiecutter-template](https://github.com/topics/cookiecutter-template)
如果你要指定特殊的主题，可以使用`cookiecutter-yourtopic`, 例如 `cookiecutter-python` 或者 `cookiecutter-datascience`。
这是GitHub的一个新特性，所以不是所有的资源库当前都可以这样使用。

If you are a template developer please add related [topics](https://help.github.com/en/github/administering-a-repository/classifying-your-repository-with-topics) with `cookiecutter` prefix to your repository.
如果你是一个模板开发人员，请使用`cookiecutter`前缀关联你的代码库[topics](https://help.github.com/en/github/administering-a-repository/classifying-your-repository-with-topics)
这样会让你的模板更容易被用户搜索到。
你几乎不会收到话题数量的限制，所以推荐你使用关联topic的功能！

### 特殊的Cookiecutter资源库

下面的Cookiecutters资源库由cookiecutter团队维护:

- [cookiecutter-pypackage](https://github.com/audreyfeldroy/cookiecutter-pypackage):
  ultimate Python package project template by [@audreyfeldroy's](https://github.com/audreyfeldroy).
- [cookiecutter-django](https://github.com/pydanny/cookiecutter-django):
  a framework for jumpstarting production-ready Django projects quickly.
  It is bleeding edge with Bootstrap 5, a customizable users app, starter templates, working user registration, celery setup, and much more.
- [cookiecutter-pytest-plugin](https://github.com/pytest-dev/cookiecutter-pytest-plugin):
  Minimal Cookiecutter template for authoring [pytest](https://docs.pytest.org/) plugins that help you to write better programs.

## 社区

核心代码提交团队: [authors' section](AUTHORS.md).
我们也欢迎并邀请您加入.

如果使用时遇到了问题，请按以下顺序来解决:

- 阅读[Troubleshooting](https://cookiecutter.readthedocs.io/en/latest/troubleshooting.html)页面.
- 在[Stack Overflow](https://stackoverflow.com/questions/tagged/cookiecutter)上查找或者提问寻求帮助.
- 强烈建议你在 [file an issue](https://github.com/cookiecutter/cookiecutter/issues?q=is%3Aopen) 页面提一个关于本问题的issue.
  大胆的去提问，不要担心无法正确的命名或者定位问题。
- 如果有必要，可以在[Discord](https://discord.gg/9BrxzPKuEW)上需求帮助。(为了大家能更多的从讨论中获益，希望你先按照前面的步骤进行排查，如果排查完依然无法解决，可以到Discord讨论).

Cookiecutter的研发是社区驱动地:

- 非常感谢所有的 [contributors](AUTHORS.md)，你们的积极参与使得Cookiecutter成为了一个更好的工具。
- 欢迎所有人参与并贡献自己的代码
  请阅读[contributing instructions](CONTRIBUTING.md), 然后就可以开始参与贡献了.
- Connect with other Cookiecutter contributors and users on [Discord](https://discord.gg/9BrxzPKuEW)
- 可以在社群[Discord](https://discord.gg/9BrxzPKuEW)上联系其他Cookiecutter作者或者用户
  (注意: 除非工作或者其他的义务, 核心提交者可能不总是在线的)

用户鼓励是对我们最大的激励.
如果你想对Cookiecutter做更多的工作以表示支持:

- 感谢核心提交者的努力
- Star [Cookiecutter on GitHub](https://github.com/cookiecutter/cookiecutter).
- [Support this project](#support-this-project)

Got criticism or complaints?
被批评或者抱怨？

- 在issue页面[File an issue](https://github.com/cookiecutter/cookiecutter/issues?q=is%3Aopen) 反馈你的问题，这样Cookiecutter就可以改善它.
  一些友好地或者建设性的意见更好。
  提出详细地建议。
- **随时向我们反馈，这样才能帮助.**
  例如，如果你讨论关于Cookiecutter的问题时，在[file an issue](https://github.com/cookiecutter/cookiecutter/issues?q=is%3Aopen)讨论问题，或者抄送给一个核心提交者。
- 请积极鼓励.
  A comment like "This function ought to be rewritten like this" is much more likely to result in action than a comment like "Eww, look how bad this function is."
  好的备注更能鼓舞开发者，譬如"这个函数应该被重写"比"这个函数非常垃圾"要更能鼓舞开发人员。

等待一个问题的反馈？

- 请耐心等待。所有的issues都在核心开发者的监控上，并且会认真考虑，但是我们有问题的待解决。
  如果情况紧急，最好是在问题上给核心开发者发送一个提醒。
- 请其他人评论、讨论、检查等
- 搜索Cookiecutter库中与你的问题相关的issue。
- 需要一个非常紧急地fix/feature/release/help?
  [@audreyfeldroy](https://github.com/audreyfeldroy) 可租用咨询或者开发

## 支持本项目

这个项目由志愿者们运维。
不久，我们将为组织和个人提供该项目的支持。

## 代码规范

Cookiecutte项目的所有代码和文档都应该遵循规范[PyPA Code of Conduct](https://www.pypa.io/en/latest/code-of-conduct/)。
包括但不限于issue trackers, chat rooms, mailing lists, and other virtual or in real-life communication.

## 创始人/主导人

本项目由[Audrey Roy Greenfeld](https://github.com/audreyfeldroy)创建与主导开发。

她得到了一组维护这支持。
