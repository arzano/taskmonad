<p align="center"><img width=17.5% src="https://raw.githubusercontent.com/mmagorsc/taskmonad/master/docs/images/taskmonad_raw.png"></p>
<p align="center"><img width=60% src="https://raw.githubusercontent.com/mmagorsc/taskmonad/master/docs/images/taskmonad_label.png"></p>

<p align="center">
<a href="https://www.haskell.org/ghc/" ><img src="https://img.shields.io/badge/ghc-8.4.1%2B-blue.svg"></a>
<a href="https://travis-ci.org/mmagorsc/taskmonad"> <img src="https://api.travis-ci.org/mmagorsc/taskmonad.svg?branch=master"></a>
<a href="https://codeclimate.com/github/mmagorsc/taskmonad"> <img src="https://api.codeclimate.com/v1/badges/e4de6996bf5bb710d0e7/maintainability"></a>
<a href="#contributing"> <img src="https://img.shields.io/badge/contributions-welcome-orange.svg"></a>
<a href="https://opensource.org/licenses/BSD-3-Clause"><img src="https://img.shields.io/badge/license-BSD-blue.svg"></a>

## Table Of Contents 

- [Basic Overview](#basic-overview)
- [Installation](#installation)
- [Usage](#usage)
- [Features](#features)
- [Documentation](#documentation)
- [Contributing](#contributing)

## Basic Overview

Basically, TaskMonad provides a collection of tools which can be used to access taskwarrior from xmonad.

<p align="center"><img width=95% src="https://raw.githubusercontent.com/mmagorsc/taskmonad/master/docs/images/taskmonad-screencast.gif"></p>


## Installation

To install Taskmonad just copy the source code into your `~/.xmonad/lib/` folder. The folder structure should afterwards look like this:

``` shell
.xmonad 
|-- lib
|   |-- Taskmonad.hs
|   |-- Taskmonad
|   |   |-- GridSelect.hs
|   |   |-- Prompt.hs
|   |   |-- ScratchPad.hs
|   |   `-- Utils.hs
|   |-- GridSelect
|   |   `-- Extras.hs
|   `-- ...
|-- xmonad.hs
```

Afterwards import TaskMonad in your `xmonad.hs`  

``` haskell
import TaskMonad
```

## Usage
To get started, add a manage hook for the taskwarrior scratchpad:

``` haskell
-- ...

... , manageHook = namedScratchpadManageHook taskwarriorScratchpads
```

After that you can bind the taskwarrior prompt to a key to get started: 

``` haskell
... , ("M-p",     taskwarriorPrompt [(\x -> x == "processInbox", processInbox)])
```

You can also bind any other TaskMonad action to a key. For example:

``` haskell
... , ("M-S-p",   taskwarriorScratchpad)       -- Opens the taskwarrior scratchpad

... , ("M-C-p",   taskSelect "status:pending") -- Displays all pending tasks

... , ("M-C-S-p", tagSelect)                   -- Displays all tags using a gridselect
```

In general you can customize the tools ad libitum. A good way to get started is to implement custom actions for the taskwarrior prompt. Please refer to taskwarriorPrompt for further information. 

## Features 

Basically TaskMonad implements a few methods which can be used to follow the GTD principles. However you can customize these methods or even implement completely different workflows. Please refer to [the documentation](https://taskmonad.magorsch.de) and [Customizing](#customizing) for further details. 

### Step 1: Capture

You can easily capture tasks, ideas or notes using the `taskwarriorPrompt` like this:

<p align="center"><img width=95% src="https://raw.githubusercontent.com/mmagorsc/taskmonad/master/docs/images/capture.png"></p>

### Step 2 & 3: Clarify & Organize

You can clarify and organize your tasks using processInbox. It implements the typical Getting Things Done workflow using GridSelects:

<p align="center"><img width=85% src="https://raw.githubusercontent.com/mmagorsc/taskmonad/master/docs/images/workflow.png"></p>


### Step 4: Reflect

You can implement your own custom daily- and weeklyreview routines. For example you can use togglePriority to adjust the priority of tasks during the daily- / weeklyreview like this:

<p align="center"><img width=95% src="https://raw.githubusercontent.com/mmagorsc/taskmonad/master/docs/images/taskmonad-gridselect.png"></p>

### Step 5: Engage

To decide which task to do next, you can use a collection of gridselects. You can use tagSelect, projectSelect, dueSelect to display a gridselect to filter the tasks by tag, project or due date. However you can also display all pending tasks using taskSelect like this:

<p align="center"><img width=95% src="https://raw.githubusercontent.com/mmagorsc/taskmonad/master/docs/images/engage.png"></p>

### Scratchpad

The taskwarrior scratchpad is used to display taskwarrior reports that have been invoked using the taskwarrior prompt. However, you can use the scratchpad at your convenience. After you have added a manage hook as described in _Installation_, you can bind a key to taskwarriorScratchpad. The Scratchpad will look like this

<p align="center"><img width=95% src="https://raw.githubusercontent.com/mmagorsc/taskmonad/master/docs/images/taskmonad-scratchpad.png"></p>

## Customizing 

TaskMonad.hs implements a few methods which are useful to use GTD. However you don't have to use any of these methods if you don't use GTD or just don't like to use them. 

TaskMonad exposes four modules which can be used to implement your own custom workflow:

- [TaskMonad.Prompt](https://taskmonad.magorsch.de/TaskMonad-Prompt.html) --      provides wrappers around XMonad.Prompt.Input for usage with taskwarrior 
- [TaskMonad.ScratchPad](https://taskmonad.magorsch.de/TaskMonad-Scratchpad.html) --  TaskMonad.ScratchPad provides a wrapper around XMonad.Util.NamedScratchpad that can be used to display taskwarrior commands 
- [TaskMonad.GridSelect](https://taskmonad.magorsch.de/TaskMonad-GridSelect.html) --  uses GridSelect.Extras to display various information from taskwarrior. 
- [TaskMonad.Utils](https://taskmonad.magorsch.de/TaskMonad-Utils.html) --       is used to communicate with taskwarrior from haskell.

You can use these modules at your convenience. However, in case please consider creating an issue or submitting a pull request so that others can also benefit from your changes.


## Documentation

The documentation of TaskMonad is generated using haddock. You can find the latest version [here](https://taskmonad.magorsch.de).

## Contributing

Contributions are welcome. You have an idea, suggestion for improvement or have found a bug? Just create an issue or send a pull request. 
