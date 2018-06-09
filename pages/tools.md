---
layout: page
title: "Tool Suite"
header: "CapiTainS Tool Suite"
group: navigation
description: ""
---
{% include JB/setup %}

**Index :**

* TOC
{:toc}

![CapiTainS](/assets/images/logo.png)

CapiTainS tool suite is large and the naming can be sometime painful to remember. Here is a reminder and description of every tool we develop.

## Python software library

### MyCapytain (Python)

[![CapiTainS MyCapytain](/assets/images/My_Capytain.png)](https://github.com/capitains/MyCapytain)

MyCapytain is a library, an abstraction for CTS. It provides simple and easy to use commands to query CTS APIs, parse replies, parse local CapiTainS based resources, as well as general classes to parse CTS URNs and References. **It's the lego brick behind all our proposed blueprint.**

**Relates resources** :

- [Documentation](https://mycapytain.readthedocs.io)
- [Nemo for Flask](#nemo-for-flask-python)
- [Nautilus for Flask](#nautilus-for-flask-python)
- [Hook](#testing-resources-hook)

## Frameworks and Softwares

### Nemo Template App

The Nemo templates app provides you with a really simple way to configure your own Nemo and Nautilus with 0 knowledge of python !

- [Nemo Template App](https://github.com/capitains/nemo-template-app)

### Nemo for Flask (Python)

[![CapiTainS Nemo for Flask](/assets/images/Nemo.png)](https://github.com/capitains/flask-capitains-nemo)

Nemo is a web frontend providing a user interface on top of a CTS API. It's highly extensible, works with templates and is based on Flask.

**Relates resources** :

- [Documentation](https://flask-capitains-nemo.readthedocs.io)
- [Tutorials](https://github.com/Capitains/tutorial-nemo/blob/master/README.md)

### Nautilus for Flask (Python)

[![CapiTainS Nautilus for Flask](/assets/images/Nautilus.png)](https://github.com/capitains/Nautilus)

Nautilus provides a backend CTS API implementation relying on local files. It provides high maintainability and good scalabilty scores.

**Relates resources** :

- [Documentation](https://capitains-nautilus.readthedocs.io)
- [Tutorials](https://github.com/Capitains/tutorial-nemo/blob/master/README.md)

## Testing resources : Hook

Hook is a suite of resources providing a test environment to check for CapiTainS guidelines compliancy of repositories. It provides tests results which can help correct resources.

### Hook Test

[![CapiTainS HookTest](/assets/images/Hook_Test.png)](https://github.com/capitains/HookTest)

HookTest is the testing software component which provides results. It can be used in other softwares but it's main goal is to be used as its own commandline tool.

**Relates resources** :

- [Validator Online App](https://capitains-validator.herokuapp.com/)
- [Docker Image](https://github.com/Capitains/docker-hooktest)
- [Installing and Running Hook easily with Docker](https://www.youtube.com/_Vmwz_761GM)

### Hook (Web User Interface)

[![CapiTainS Hook](/assets/images/Hook.png)](https://github.com/capitains/Hook)

This app is providing a frontend for tracking tests results and github repositories on a hosting plan. Tracks and provide more insight based on tests run on other machines.

**Related resources** :

- [Perseids Implementation](http://ci.perseids.org)


## Sparrow (JavaScript)

[![CapiTainS Sparrow](/assets/images/Sparrow.png)](https://github.com/capitains/Sparrow)

CapiTainS Sparrow is a library, an abstraction for CTS. It provides simple and easy-to-use commands to query CTS APIs as well as parsing results resources.
