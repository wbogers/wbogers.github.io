---
layout: post
title: Visual Studio Code as a Python IDE
subtitle: Setting up a productive environment
tags: [Python, Visual Studio Code, Spyder, IDE]
---

When I’m programming in Python I usually use [Spyder](https://www.spyder-ide.org), The Scientific Python Development Environment. It’s a very powerful, specialized, feature rich Python IDE which supports all the things you normally need as a Python developer (autocomplete, intellisense, static code analysis, debugging, terminals, IPython consoles, integrated documentation and so on). I originally picked up Spyder because it is included in the [Anaconda](https://docs.anaconda.com/anaconda/) distribution which I have installed on my laptop. Since I liked it a lot, it’s now part of my standard set of Python tools, other tools being the [Jupyter Notebook](https://jupyter.org) and, more recently, [JupyterLab](https://github.com/jupyterlab)). Spyder is under active development and keeps getting better with each release: the upcoming version 4 promises to have a lot of good stuff in it, you can read a little bit about it [here](https://www.spyder-ide.org/blog/spyder-status-2018-present/). In my opinion Spyder is a rock solid IDE which enables you to get your stuff done and I can highly recommend using it.

Still, quite recently I started using [Visual Studio Code](https://code.visualstudio.com). The main reason for this was very simple: I was curious. Visual Studio Code has been getting a lot of attention lately as a flexible, extensible, lightweight code editor and I wanted to check whether it would be an interesting tool to add to my Python toolset. For this, it would have to enable me to basically be as productive as I am in Spyder. I must say I was very pleasantly surprised with what Visual Studio Code had to offer after I had found and installed the right extensions. So I want to share some of my experiences about getting Visual Studio Code up and running as a Python IDE.

I initially installed Visual Studio Code just before the July 2018 release. After installing Microsoft’s Python extension I gave it a try and must admit that at first I wasn’t very wowed: as an editor it was pleasant enough to work in, but considering the Spyder experience I was used to it just didn’t do it for me at that moment (especially features like autocomplete and intellisense felt a bit off). However, a couple of weeks later the July 2018 release came along with a *huge* amount of added and improved Python support. One of the most important additions was the  [Python Language Server](https://blogs.msdn.microsoft.com/pythonengineering/2018/07/18/introducing-the-python-language-server/): allthough it was an early version which was included in this release of Visual Studio Code, for me it completely changed the way the editor felt when working with Python. After installing a few additional extensions and tweaking the layout a bit I now find Visual Studio Code to be a very pleasant, fluent environment for Python programming. Below I will describe my setup. Note that I’m working on a MacBook: on a Windows machine there are some small differences (which I will add shortly).

## Extensions

Extensions can be installed from the Marketplace by clicking on the *Extensions* button in the side bar, which in the standard setup is on the left side of the screen. See the screenshot below.

![extensions](/img/VSCode_extensions.jpeg)

I have installed only three extensions to get the Python experience I like: Microsoft’s own Python extension (including the Python Language Server I mentioned before), an extension for generating Python docstrings (in various formats) and an extension for viewing Excel and csv-files (always handy to have one of those). The table below shows some details.

Extension | Version | Author | Description
--------- | ------- | ------ | -----------
Python | 2018.7.1 | Microsoft | Linting, Debugging (multi-threaded, remote), Intellisense, code formatting, refactoring, unit tests, snippets, and more.
autoDocString | 0.2.3 | Nils Werner | Generates python docstrings.
Excel Viewer | 2.1.26 | GrapeCity | View Excel spreadsheets and CSV files within Visual Studio Code workspaces.

The versions mentioned are the versions at the time of me writing this. As can be seen from the description of Microsoft’s Python extension it bundles a lot of functionality. It’s important to change a couple of configuration options in the *User Settings* in order to get the best (in my opinion) experience. The options I changed are described in the next section. It's good to know that Microsoft's Python extension uses *Pylint* as its standard linter (allthough other linters like *Flake8* and *Pep8* are also supported). For me *Pylint* serves my needs, so I don’t need to change the default settings.

Note that I have tried a couple of other Python related extensions, but for me they didn't add anything at the moment. But there’s lot to explore in the Marketplace, just check out what suits your personal preferences the best.

## Configuration options

I changed the following settings in *User Settings*:

Setting | Value | Description
------- | ----- | -----------
python.jediEnabled | false | Necessary for using the Python Language Server.
python.linting.pylintUseMinimalCheckers | false | Make sure all problems are reported.
python.pythonPath | /../anaconda/envs/*env_name*/bin/python | Path to Python executable in desired conda environment.
autoDocstring.docstringFormat | “google” | Use Google’s docstring layout.
csv-preview.separator | “;” | Use ; as a field separator.

The first three settings are specific to Microsoft's Python extension, the fourth setting is for the autoDocString extension and the last setting sets the default separator for the Excel Viewer extension. Note that the *python.pythonPath* setting guarantees that I always execute code in the desired conda environment. It is also possible to choose a specific Python version / environment to use on the fly by entering *Python: Select Interpreter command* in the *Command Palette*, but I like things to be set up from the start.

The settings above are directly related to the behaviour of the installed extensions. I also have several settings which change the look and feel of the Visual Studio Code window to my liking:

Setting | Value | Description
------- | ----- | -----------
editor.fontSize | 10 | Smaller font size, suitable for me.
python.autoComplete.preloadModules | ["Numpy", "Pandas", "Matplotlib”] | Preload some big modules.
workbench.colorTheme | "Tomorrow Night Blue" | Gorgeous color theme.

Note that there are tons of configuration options available to customize Visual Studio Code to your personal preference. You can explore the (very well documented) *User Settings* for this.

## Layout

I always want to have a terminal and an IPython console active in my workspace. This can be achieved by activating a terminal, splitting it and running IPython in the second terminal. Because I use conda environments, this means that I first run *source activate env* in the second terminal to activate the desired environment (with *env* the actual environment name) and then run *ipython*.

So eventually I end up with the following layout in my Visual Studio Code window:

![workspace](/img/VSCode_workspace.jpeg)

Problems are reported in the *Problems* panel:

![problems](/img/VSCode_problems.jpeg)

All in all this is an environment that is very nice to code in and which feels very smooth. I like it a lot (and use it almost exclusively lately).

## Functionality

So what do we have after setting up the environment as described above? We have autocomplete and intellisense, we have a fast, complete linter, great debugging support, support for unit tests, terminals, IPython consoles, an outline view and a minimap of the code you’re working on. Personally I think it all looks very organized and nice on screen and it really invites you to start coding. Right clicking in a code window brings up a context menu with useful commands, for example:

* **Run Python File in Terminal**: runs the code, activating the selected conda environment if necessary.
* **Format Document**: formats the code, prevents a lot of linter warnings (concerning whitespace, extra lines and so on).
* **Generate Docstring**: added by the autoDocString extension, creates docstring for selected function.

All commands mentioned above can ofcourse be activated using keyboard shortcuts, and there are a lot more than those mentioned here. Note that commands can also be run from the *Command Palette*.

## Conclusion


I think Visual Studio Code is an awesome editor for Python coding, at least for the things I usually do with Python (mainly solving data oriented problems): I just love it. So together with Spyder I now have two great IDE's to work with, Visual Studio Code being the one I use most of the time recently. Combine this with the power of Jupyter notebooks for interactive, narrative data science stuff and I must say that I can pretty much tackle all problems that I encounter. Python coding is always fun, but with these kinds of tools it's a real joy to take on all kinds of challenges.

## Additional resources

[Philosophy of Visual Studio Code](https://code.visualstudio.com/docs/editor/whyvscode)
