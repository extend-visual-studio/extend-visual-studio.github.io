## Welcome

This site, extendvs.com, has a simple mission: to expand the public knowledge based for building extensions for Visual Studio Windows and Mac.

extenvs.com is an open source, MIT licensed, community-led site.

## Extension Samples

Please find a list of extension samples

## Overview

This sections provides an overview of the common concepts in an IDE extension and what the equivalant API/object is in the other IDE.

### Manifests

The *manifest* declares the information about our extension such as its name, author, copyright, identifier and version number.

**Visual Studio Windows**

A Visual Studio Windows extension has two manifest files, the `vsix` manifest and the command manifest.

 *

**Visual Studio Mac**

A Visual S

To declare the name, version and

The extension manifest is the `Manifest.addin.xml`

### Package

The *package* is the central class that represents our extension and exposes it to the IDE.

**Visual Studio Windows**
The `AsyncPackage` class is the

**Visual Studio Mac**
Visual Studio Mac does not have the concept of a core package class.

### Package Startup

The package startup

**Visual Studio Windows**

**Visual Studio Mac**




### IDE Application

The IDE application is the root access point for most of the major APIs we would use in our extension.

**Visual Studio Windows**

In Visual Studio Windows the root IDE/application object is the [DTE]().

```
```

**Visual Studio Mac**

In Visual Studio Mac, the root IDE/application object is the IdeApp.

```
MonoDevelop.Ide.IdeApp;

```

### Service Locator

The *service locator* is used to retrieve service implementations through a central access class.

**Visual Studio Windows**
In Visual Studio Windows, the service locator is the `ServiceProvider` class.

**Visual Studio Mac**
Visual Studio Mac does not have a service locator.

To access core services:

 * Use the static `IdeServices` to access core services like the ProjectService, TypeSystemService, DesktopService etc.
 * Use the `CompositionManager` to access parts that have been exported to MEF.
 * Use the `IdeApp` to access the core services such as the Workspace, Workbench

### Composition Manager

The *composition manager* is used to retrieve parts that are exported to the Managed Extensibility Framework.

**Visual Studio Windows**

**Visual Studio Mac**

### Commands

* **Visual Studio Windows**: OleCommand
* **Visual Studio Mac**: CommandHandler.

### Active Document

* **Visual Studio Windows**:
* **Visual Studio Mac**:

### Running Document Table
The runnign document table is used to describe which documents are currently open and


### Workspace Model
In IDE extensions we have the concept of a *workspace model*, that is, the hierachical relationship of a solution, its projects and then those projects files and references.

The *workspace model* is different to the *compilation model* as it

### Workspace Events

### Solution Pad/Explorer

### Pads
