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

CapiTainS tool suite is large and the naming can be sometime painful to remember. Here is a reminder and description of every tool we develop.

## Language Libraries

### Sparrow (JavaScript)

[![CapiTainS Sparrow](/assets/images/Sparrow.png)](https://github.com/capitains/Sparrow)

CapiTainS Sparrow is a library, an abstraction for CTS. It provides simple and easy-to-use commands to query CTS APIs as well as parsing results resources.

**Relates resources** :

- [Documentation](https://github.com/Capitains/docker-hooktest)
- [jQuery Typeahead](https://github.com/Capitains/jQuery.typeahead) retrieve resources and passages using a simple fulltext search tool on CTS inventories.
- [Journey Of The Hero](http://www.perseids.org/sites/joth/) was developed using full frontend technologies and Sparrow for CTS API communication and parsing
- [jQuery Selector plugin](https://github.com/Capitains/jQuery.selector) : list resources and retrieve them using form boxes *(Development on hold)*
- [jQuery Service Plugin](https://github.com/Capitains/jQuery.service) implements a simple way to call API Services using CTS data *(Development on hold)*
- [jQuery XSLT Plugin](https://github.com/Capitains/jQuery.xslt) implements a simple way to use XSLT (with parameters) using CTS Data *(Development on hold)*
- [Nemo for AngularJS](https://github.com/angular-nemo) was a quick demo tool to show the potential uses of Sparrow *(Development on hold)*

### MyCapytain (Python)

[![CapiTainS MyCapytain](/assets/images/My_Capytain.png)](https://github.com/capitains/MyCapytain)

MyCapytain is a library, an abstraction for CTS. It provides simple and easy to use commands to query CTS APIs, parse replies, parse local CapiTainS based resources, as well as general classes to parse CTS URNs and References.

**Relates resources** :

- [Documentation](https://mycapytain.readthedocs.io)
- [Nemo for Flask](#nemo-for-flask-python)
- [Nautilus for Flask](#nautilus-for-flask-python)
- [Nautilus for Flask](#nautilus-for-flask-python)
- [Hook](#testing-resources-hook)

### Cavern (Ruby)

![CapiTainS Cavern](/assets/images/Cavern.png)

*In development by Perseids' developer Bridget Almas*

## Frameworks and Softwares

### Nemo for Flask (Python)

[![CapiTainS Nemo for Flask](/assets/images/Nemo.png)](https://github.com/capitains/flask-capitains-nemo)

Nemo is a web frontend providing a user interface on top of a CTS API. It's highly extensible, works with templates and is based on Flask.

**Relates resources** :

- [Documentation](https://flask-capitains-nemo.readthedocs.io)
- [Docker Image with Nautilus](https://github.com/Capitains/docker-capitains-nemo-nautilus) ([Tutorials](/pages/tutorials.html))

### Nautilus for Flask (Python)

[![CapiTainS Nautilus for Flask](/assets/images/CTS_API.png)](https://github.com/capitains/Nautilus)

Nautilus provides a backend CTS API implementation relying on local files. It provides high maintainability and good scalabilty scores.

**Relates resources** :

- [Documentation](https://capitains-nautilus.readthedocs.io)
- [Docker Image with Nemo](https://github.com/Capitains/docker-capitains-nemo-nautilus) ([Tutorials](/pages/tutorials.html))

### CTS API for eXistDB (xQuery)

[![CapiTainS CTS API for eXistDB](/assets/images/CTS_API.png)](https://github.com/capitains/CTS5-XQ)

eXistDB Package which provide a CTS API *(Development on hold)*

### Inventory Maker for eXistDB (xQuery)

[![CapiTainS Inventory Maker for eXistDB](/assets/images/Inventory_Maker.png)](https://github.com/capitains/inventory-maker)

eXistDB Package which provide an admin interface for building inventories *(Development on hold)*

### Ahab for eXistDB (xQuery)

[![CapiTainS Ahab](/assets/images/Ahab.png)](https://github.com/capitains/Ahab-eXistDB)

eXistDB Package which provide an Ahab API *(Development on hold)*

## Testing resources : Hook

Hook is a suite of resources providing a test environment to check for CapiTainS guidelines compliancy of repositories. It provides tests results which can help correct resources.

### Hook (Web User Interface)

[![CapiTainS Hook](/assets/images/Hook.png)](https://github.com/capitains/Hook)

This app is providing a frontend for tracking tests results and github repositories on a hosting plan. It provides user account, continuous integration test to connect with Github repositories : Push and Pull Requests triggers automatic tests through this UI.

**Related resources** :

- [Perseids Implementation, with Humboldt DH Chair as computing time provider](http://ci.perseids.org)


### Hook Worker and Hook API

[![CapiTainS HookWorker](/assets/images/Hook_Worker.png)](https://github.com/capitains/Hook-Worker)

Hook-Worker is a component which provides a simple API interface to dispatch test to a Redis Queue so that tests are run on a machine. It allows to explicitly dispatch concerns between the UI, the Tests Queue and the Test Machines.

**Relates resources** :

- [Documentation](http://hook-worker.readthedocs.io/en/latest/?badge=latest)

### Hook Test

[![CapiTainS HookTest](/assets/images/Hook_Test.png)](https://github.com/capitains/HookTest)

HookTest is the testing software component which provides results. It can be used in other softwares (such as HookTest) or used as its own commandline tool.

**Relates resources** :

- [Docker Image](https://github.com/Capitains/docker-hooktest)
- [Installing and Running Hook easily with Docker](https://www.youtube.com/_Vmwz_761GM)

## Other resources

Other resources such as guidelines tools are developed on the side :

- [CookieCutter Capitains](https://github.com/Capitains/docker-cookiecutter-guidelines) provides a simple way to kickstart a repository using CookieCutter.