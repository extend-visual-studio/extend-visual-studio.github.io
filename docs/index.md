## Welcome

This site, extendvs.com, has a simple mission: to expand the public knowledge based for building extensions for Visual Studio Windows and Mac.

extenvs.com is an open source, MIT licensed, community-led site. Please contribute and help grow the knowledge base for Visual Studio extensibility.

## Overview

This sections provides an overview of the common concepts in an IDE extension and what the equivalant API/object is in the other IDE.

### Manifests

The *manifest* declares the information about our extension such as its name, author, copyright, identifier and version number.

**Visual Studio Windows**

A Visual Studio Windows extension has the VSIX manifest and the command manifest.

 * The VSIX manifest file (`extension.vsixmanifest`) defines the information about your extension such as name, author, version number and more. [See here for documentation.](https://docs.microsoft.com/en-us/visualstudio/extensibility/anatomy-of-a-vsix-package?view=vs-2019)
 * The Visual Studio Command Table (`.vsct`) defines the commands that your package contains. [See here for documentation.](https://docs.microsoft.com/en-us/visualstudio/extensibility/internals/visual-studio-command-table-dot-vsct-files?view=vs-2019)

**Visual Studio Mac**

A Visual Studio Mac extension includes a file named `Manifest.addin.xml` that defines the extension points

To declare the name, author, copyright, version etc of an extension, we use the following attributes:

### Package

The *package* is the central class that represents our extension and exposes it to the IDE.

**Visual Studio Windows**
We implement the `AsyncPackage` class to declare the core of our extension. [See here for documentation.](https://docs.microsoft.com/en-us/visualstudio/extensibility/how-to-use-asyncpackage-to-load-vspackages-in-the-background?view=vs-2019)

**Visual Studio Mac**
Visual Studio Mac does not have the concept of a core package class.

### Extension Startup

For both Visual Studio Windows and Mac, extensions by default do not have a defined entry point. Extensions do not receive startup notifications by default and should be design so that they do not rely on a startup sequence.

**Visual Studio Windows**
To detect the startup of our extension in Visual Studio Windows, we register the loading of our package against a specified IDE event using the `ProvideAutoLoad` attribute attached to our Package.

[See here for documentation](https://docs.microsoft.com/en-us/visualstudio/extensibility/loading-vspackages?view=vs-2019).

!!! info "Avoid relying on any form of startup event to initialise your Visual Studio Windows extension. The modern Visual Studio APIs (such as IntelliSense or adornments) and Roslyn APIs load feature implementations outside of "

**Visual Studio Mac**

To detect the startup of our extension on Visual Studio Mac, we add a new `CommandHandler` to the `/MonoDevelop/Ide/StartupHandlers` extension point.

### IDE Application

The IDE application is the root access point for most of the major APIs we would use in our extension.

**Visual Studio Windows**

In Visual Studio Windows the root IDE/application object is the [DTE](https://docs.microsoft.com/en-us/dotnet/api/envdte.dte?view=visualstudiosdk-2017).

Importantly, the DTE also has the [DTE2](https://docs.microsoft.com/en-us/dotnet/api/envdte80.dte2?view=visualstudiosdk-2017) interface that exposes many additional APIs.

**Visual Studio Mac**

In Visual Studio Mac, the root IDE/application object is the `IdeApp`.

### Service Locator

The *service locator* is used to retrieve service implementations through a central access class.

**Visual Studio Windows**
In Visual Studio Windows, the service locator is the `ServiceProvider` class.

Below is an example of retrieving a service using the `ServiceProvider`:
```
var dte = ServiceProvider.GlobalProvider.GetService(typeof(DTE)) as DTE2;
```

**Visual Studio Mac**
Visual Studio Mac does not have a service locator.

To access core services:

 * Use the static `IdeServices` to access core services like the ProjectService, TypeSystemService, DesktopService etc.
 * Use the `CompositionManager` to access parts that have been exported to MEF.
 * Use the `IdeApp` to access the core services such as the Workspace, Workbench

### Composition Manager

The *composition manager* is used to retrieve parts that are exported to the Managed Extensibility Framework.

**Visual Studio Windows**
We can access the MEF composition manager on Windows with the following code:

```
```

**Visual Studio Mac**
We can access the MEF composition manager on Mac with the following code:

```
```

### Commands

**Visual Studio Windows**
In Visual Studio Windows we declare command elements in a `vsct` file and register new commands using the `OleMenuCommandService`.

[See here for documentation.](https://docs.microsoft.com/en-us/visualstudio/extensibility/extending-menus-and-commands?view=vs-2019)

**Visual Studio Mac**
In Visual Studio Mac we create `CommandHandler` sub-classes and then connect that command instance into an extension point using the `Manifest.addin.xml` file.

[See here for documentation.](https://docs.microsoft.com/en-us/visualstudio/mac/extending-visual-studio-mac?view=vsmac-2019#extensions-and-extension-points)

### Active Documents
The list of active, opened documents, also known as the running documents table, describe the documents that are currently open and have a source code editor user interface.

**Visual Studio Windows**
In Visual Studio Windows, we can the [`DTE2.Documents`](https://docs.microsoft.com/en-us/dotnet/api/envdte80.dte2.documents?view=visualstudiosdk-2017#EnvDTE80_DTE2_Documents) property to access the currently open documents.

To subscribe to document open/closed/modified events, we can use the [`DTE2.Events.DocumentEvents`](https://docs.microsoft.com/en-us/dotnet/api/envdte.documentevents?view=visualstudiosdk-2017) property.

**Visual Studio Mac**
In Visual Studio Mac, we can use the `TypeSystemService.DocumentManager` to query the currently opened documents and subscribe to open/closed/modified events.

### Workspace Model
In IDE extensions we have the concept of a *workspace model*, that is, the hierarchical relationship of a solution, its projects and the files and references of those projects.

The *workspace model* is different to the *compilation model* as it incorporates project assets (like images or embedded resources), packages etc into the model. The *workspace model* is akin to what is displayed in the Solution Explorer, whereas the *compilation model* only contains information required to generate an executable.

**Visual Studio Windows**

**Visual Studio Mac**

### Workspace Events

### Solution Pad/Explorer

### Pads
