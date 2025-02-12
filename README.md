<br/>
<div id="che-theia-logo" align="center" style="vertical-align: middle">

<img src="https://raw.githubusercontent.com/eclipse/che-theia/master/extensions/eclipse-che-theia-about/src/browser/style/che-logo-light.svg?sanitize=true" alt="Che Logo" width="200" />

<img src="https://raw.githubusercontent.com/theia-ide/theia/master/logo/theia-logo.svg?sanitize=true" alt="Theia Logo" width="150"/>

# Che Theia


</div>

<div id="badges" align="center">

  [![Build Status](https://ci.codenvycorp.com/buildStatus/icon?job=che-theia-master-ci)](https://ci.codenvycorp.com/job/che-theia-master-ci)
  [![mattermost](https://img.shields.io/badge/chat-on%20mattermost-blue.svg)](https://mattermost.eclipse.org/eclipse/channels/eclipse-che-ide2-team)
  [![Open questions](https://img.shields.io/badge/Open-questions-blue.svg?style=flat-curved)](https://github.com/eclipse/che-theia/labels/kind%2Fquestion)
  [![Open bugs](https://img.shields.io/badge/Open-bugs-red.svg?style=flat-curved)](https://github.com/eclipse/che-theia/labels/kind%2Fbug)

</div>

<div style='margin:0 auto;width:80%;'>

![Che-Theia](https://raw.githubusercontent.com/eclipse/che-theia/master/che-theia-screenshot.png)

</div>

## What is Che-theia ?
[Eclipse Che](https://eclipse.org/che/) provides a default web IDE for the workspaces which is based on the [Theia](https://github.com/theia-ide/theia) project. It’s a subtle different version than a plain  Theia(https://github.com/theia-ide/theia) as there are functionalities that have been added based on the nature of the Eclipse Che workspaces. We are calling this version of Eclipse Theia for Che: Che-Theia.

So, Che-Theia is the default `Che editor` provided with developer workspaces created in [Eclipse Che 7](https://eclipse.org/che/)([Github](https://github.com/eclipse/che)).

Che-Theia contains additional extensions and plugins which have been added based on the nature of Eclipse Che workspaces and to provide the best IDE experience of Theia within Che.
 - A VSCode-like IDE experience. Che-Theia is based on the monaco
   editor and includes features like the command pallete.
 - VSCode extension compatibility. Che-Theia supports VSCode
   extensions. In Che-theia, these extensions could come with a side-car
   containers with all the dependencies required by the extension.
   No need to install the JDK or Maven when you install our VSCode Java plugin.
 - Nice views to interact with your user containers or production runtime containers.
   (Terminal access, execute Che-commands in specific containers, etc...)

## Che-Theia capabilities
In Che-Theia, you’ll find the following capabilities:


| Plug-in               | Description |
|-----------------------|-------------|
| Che Extended Tasks    | Handles the Che commands and provides the ability to start those into a specific container of the workspace. |
| Che Extended Terminal | Allows to provide terminal for any of the containers of the workspace. |
| Che Factory           | Handles the Eclipse Che Factories [TODO: LINK] |
| Che Container         | Provides a container view that shows all the containers that are running in the workspace and allows to interact with them. |
| Che Dashboard         | Allows to integrate the IDE with Che Dashboard and facilitate the navigation. |
| Che Welcome Page      | Display a welcome page with handy links when opening the IDE. |
| Che Ports             | Allows to detect when services are running inside of the workspace and expose them. |
| Che APIs              | Extends the IDE APIs, to allow interacting with the Che specific components (workspaces, preferences, etc.). |


## Join the community

The Eclipse Che community is globally reachable through public chat rooms, mailing list and weekly calls.
See https://www.eclipse.org/che/docs/che-7/introduction-to-eclipse-che.html#joining-the-community

Che-Theia is mainly maintained by the Che IDE2 team a.k.a Selene.
You are very welcome to join our community chat [here](https://mattermost.eclipse.org/eclipse/channels/eclipse-che-ide2-team) to discuss about improvements, bug fixes and anything else.

## Project structure

- [che-plugins](./che-plugins) contains Eclipse Che plugins definition
- [dockerfiles](./dockerfiles) contains Dockerfiles
- [extensions](./extensions) contains Theia Extensions
- [plugins](./plugins) contains Theia Plugins

# Contributing
## How to build

Run `yarn` to build Theia extensions and plugins.

> Note: this build Theia extensions and plugins __ONLY__

If you want to build all images also run `build.sh` script.

CI for PR job in this repository will use `build.sh --pr`.
> Note: `--pr` will build only limited set of docker images, see [PR_IMAGES variable](./docker_image_build.include)

If you want to publish docker images use `build.sh --push`

## How to build own che-theia image

First you need to build `che-theia-dev` image:

Run in `dockerfiles/theia-dev` dir:

```bash
    ./build.sh --build-arg:${GITHUB_TOKEN_ARG} --tag:next
```

Then in `dockerfiles/theia` run:

```bash
./build.sh --build-args:${GITHUB_TOKEN_ARG},THEIA_VERSION=master --tag:next --branch:master --git-ref:refs\\/heads\\/master
```

Where `${GITHUB_TOKEN_ARG}` is your GitHub API token, it's used for fetching some vscode library that placed on GitHub releases, without that token build may fail.

That script will clone Theia from master branch and all Che related extensions from theirs master branches.


## License

- [Eclipse Public License 2.0](LICENSE)
