<p align="center">
<img align="center" src="https://github.com/pipxproject/pipx/raw/master/logo.png"/>
</p>

# pipx: execute binaries from Python packages in isolated environments

<p align="center">
<a href="https://github.com/pipxproject/pipx/raw/master/pipx_demo.gif">
<img src="https://github.com/pipxproject/pipx/raw/master/pipx_demo.gif"/>
</a>
</p>

<p align="center">
<a href="https://travis-ci.org/pipxproject/pipx"><img src="https://travis-ci.org/pipxproject/pipx.svg?branch=master" /></a>

<a href="https://pypi.python.org/pypi/pipx/">
<img src="https://img.shields.io/badge/pypi-{{version}}-blue.svg" /></a>
<a href="https://github.com/ambv/black"><img alt="Code style: black" src="https://img.shields.io/badge/code%20style-black-000000.svg"></a>
</p>

_For comparison to pipsi, see the [FAQ](faq.md)._

_pipx uses the word "binary" to describe a CLI application that can be run directly from the command line. These files are located in the `bin` directory of a Python installation, alongside other executables. Despite the name, they do not necessarily contain binary data._

## Install pipx

```
python3 -m pip install --user pipx
python3 -m pipx ensurepath
```

For more details, see [installation](installation).

## Overview

Python and PyPI allow developers to distribute code with "console script entry points". These scripts let users call into Python code from the command line, effectively acting like standalone applications.

`pipx` is a tool to install and run any of the thousands of Python applications available on PyPI in a safe, convenient, and reliable way. Not all Python packages have entry points, but many do.

`pipx` lets you:

- Safely install packages to isolated virtual environments, while globally exposing their CLI entry points so you can run them from anywhere (see the `install` command)
- Easily list, upgrade, and uninstall packages that were installed with pipx
- Run the latest version of a CLI application in a temporary environment (see the `run` command)
- Run binaries from the `__pypackages__` directory per PEP 582 as a companion tool to [pythonloc](https://github.com/cs01/pythonloc)

Best of all, pipx runs with regular user permissions, never calling `sudo pip install` (you aren't doing that, are you? 😄).

pipx is similar to JavaScript's [npx](https://medium.com/@maybekatz/introducing-npx-an-npm-package-runner-55f7d4bd282b) - which ships with npm, but also allows you to install instead of just run. pipx does not ship with pip but installing it is often an important part of bootstrapping your system.

### Safely installing to isolated environments

You can globally install a CLI application by running

```
pipx install PACKAGE
```

This automatically creates a virtual environment, installs the package, and adds the package's CLI entry points to a location on your `PATH`. For example, `pipx install pycowsay` makes the `pycowsay` command available globally, but sandboxes the pycowsay package in its own virtual environment. **pipx never needs to run as sudo to do this.**

Example:

```
>> pipx install pycowsay
  installed package pycowsay 2.0, Python 3.6.7
  These binaries are now globally available
    - pycowsay
done! ✨ 🌟 ✨

>> pipx list
venvs are in /home/user/.local/pipx/venvs
binaries are exposed on your $PATH at /home/user/.local/bin
   package pycowsay 2.0, Python 3.6.7
    - pycowsay

>> pycowsay moooo
  _____
< moooo >
  =====
          \
           \
             ^__^
             (oo)\_______
             (__)\       )\/       ||----w |
                 ||     ||
```

### Running in temporary, sandboxed environments

pipx makes running the latest version of a program in a temporary environment as easy as

```
pipx run BINARY [ARGS...]
```

This will install the package in an isolated, temporary directory and invoke the binary. Try it!

```
pipx run pycowsay moo
```

Notice that you **don't need to execute any install commands to run the binary**.

Re-running the same binary is quick because pipx caches Virtual Environments on a per-binary basis. These caches last two days.

You can run .py files directly, too.

```
pipx run https://gist.githubusercontent.com/cs01/fa721a17a326e551ede048c5088f9e0f/raw/6bdfbb6e9c1132b1c38fdd2f195d4a24c540c324/pipx-demo.py
pipx is working!
```

## Testimonials

"Thanks for improving the workflow that pipsi has covered in the past. Nicely done!"
— [Jannis Leidel](https://twitter.com/jezdez) PSF fellow and former pip maintainer

"Just the “pipx upgrade-all” command is already a huge win over pipsi"
— [Stefane Fermigier](https://twitter.com/sfermigier/status/1093073303521116160)

"This tool filled in the gap that was missing with pipenv and Virtual Environmentwrapper."
— [Mason Egger](https://medium.com/homeaway-tech-blog/simplify-your-python-developer-environment-aba90f32dddb)

## Credits

pipx was inspired by [pipsi](https://github.com/mitsuhiko/pipsi) and [npx](https://github.com/zkat/npx).

- [Chad Smith](https://github.com/cs01/), creator and maintainer
- [Bjorn Neergaard](https://github.com/neersighted), contributor
- [Diego Fernandez](https://github.com/aiguofer), contributor
- [tkossak](https://github.com/tkossak), contributor
- [Shawn Hensley](https://github.com/sahensley), contributor
