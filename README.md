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

- 当你没有显示的使用`--no-input`时，系统会提示你输入:
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
- Pre- and post-generate hooks: Python or shell scripts to run before or after generating a project.

## Available Cookiecutters

Making great cookies takes a lot of cookiecutters and contributors.
We're so pleased that there are many Cookiecutter project templates to choose from.
We hope you find a cookiecutter that is just right for your needs.

### A Pantry Full of Cookiecutters

The best place to start searching for specific and ready-to-use cookiecutter templates is [Github search](https://github.com/search?q=cookiecutter&type=Repositories).
Just type `cookiecutter` and you will discover over 4000 related repositories.

We also recommend you check related GitHub topics.
For general search use [cookiecutter-template](https://github.com/topics/cookiecutter-template).
For specific topics try to use `cookiecutter-yourtopic`, like `cookiecutter-python` or `cookiecutter-datascience`.
This is a new GitHub feature, so not all active repositories use it at the moment.

If you are a template developer please add related [topics](https://help.github.com/en/github/administering-a-repository/classifying-your-repository-with-topics) with `cookiecutter` prefix to your repository.
We believe it will make it more discoverable.
You are almost not limited in topic amount, use it!

### Cookiecutter Specials

These Cookiecutters are maintained by the cookiecutter team:

- [cookiecutter-pypackage](https://github.com/audreyfeldroy/cookiecutter-pypackage):
  ultimate Python package project template by [@audreyfeldroy's](https://github.com/audreyfeldroy).
- [cookiecutter-django](https://github.com/pydanny/cookiecutter-django):
  a framework for jumpstarting production-ready Django projects quickly.
  It is bleeding edge with Bootstrap 5, a customizable users app, starter templates, working user registration, celery setup, and much more.
- [cookiecutter-pytest-plugin](https://github.com/pytest-dev/cookiecutter-pytest-plugin):
  Minimal Cookiecutter template for authoring [pytest](https://docs.pytest.org/) plugins that help you to write better programs.

## Community

The core committer team can be found in the [authors' section](AUTHORS.md).
We are always welcome and invite you to participate.

Stuck? Try one of the following:

- See the [Troubleshooting](https://cookiecutter.readthedocs.io/en/latest/troubleshooting.html) page.
- Ask for help on [Stack Overflow](https://stackoverflow.com/questions/tagged/cookiecutter).
- You are strongly encouraged to [file an issue](https://github.com/cookiecutter/cookiecutter/issues?q=is%3Aopen) about the problem.
  Do it even if it's just "I can't get it to work on this cookiecutter" with a link to your cookiecutter.
  Don't worry about naming/pinpointing the issue properly.
- Ask for help on [Discord](https://discord.gg/9BrxzPKuEW) if you must (but please try one of the other options first, so that others can benefit from the discussion).

Development on Cookiecutter is community-driven:

- Huge thanks to all the [contributors](AUTHORS.md) who have pitched in to help make Cookiecutter an even better tool.
- Everyone is invited to contribute.
  Read the [contributing instructions](CONTRIBUTING.md), then get started.
- Connect with other Cookiecutter contributors and users on [Discord](https://discord.gg/9BrxzPKuEW)
  (note: due to work and other commitments, a core committer might not always be available)

Encouragement is unbelievably motivating.
If you want more work done on Cookiecutter, show support:

- Thank a core committer for their efforts.
- Star [Cookiecutter on GitHub](https://github.com/cookiecutter/cookiecutter).
- [Support this project](#support-this-project)

Got criticism or complaints?

- [File an issue](https://github.com/cookiecutter/cookiecutter/issues?q=is%3Aopen) so that Cookiecutter can be improved.
  Be friendly and constructive about what could be better.
  Make detailed suggestions.
- **Keep us in the loop so that we can help.**
  For example, if you are discussing problems with Cookiecutter on a mailing list, [file an issue](https://github.com/cookiecutter/cookiecutter/issues?q=is%3Aopen) where you link to the discussion thread and/or cc at least 1 core committer on the email.
- Be encouraging.
  A comment like "This function ought to be rewritten like this" is much more likely to result in action than a comment like "Eww, look how bad this function is."

Waiting for a response to an issue/question?

- Be patient and persistent. All issues are on the core committer team's radar and will be considered thoughtfully, but we have a lot of issues to work through.
  If urgent, it's fine to ping a core committer in the issue with a reminder.
- Ask others to comment, discuss, review, etc.
- Search the Cookiecutter repo for issues related to yours.
- Need a fix/feature/release/help urgently, and can't wait?
  [@audreyfeldroy](https://github.com/audreyfeldroy) is available for hire for consultation or custom development.

## Support This Project

This project is run by volunteers.
Shortly we will be providing means for organizations and individuals to support the project.

## Code of Conduct

Everyone interacting in the Cookiecutter project's codebases and documentation is expected to follow the [PyPA Code of Conduct](https://www.pypa.io/en/latest/code-of-conduct/).
This includes but is not limited to, issue trackers, chat rooms, mailing lists, and other virtual or in real-life communication.

## Creator / Leader

This project was created and led by [Audrey Roy Greenfeld](https://github.com/audreyfeldroy).

She is supported by a team of maintainers.
