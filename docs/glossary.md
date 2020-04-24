!!! quote "A glossary of core terminology for Visual Studio extension development"

## Common Terminology

### Integrated Development Environment (IDE)

An application for software developers that provides code editing, debugging and compilation features.

### Inversion Of Control (IOC)

### Dependency Injection (DI)

## Visual Studio Windows

## Visual Studio Mac

## Roslyn

## Managed Extensibility Framework

### Managed Extensibility Framework (MEF)

A library for creating lightweight, extensible applications.

MEF is an Inversion Of Control framework that provides component/part management and dependency injection and is the backing IOC technology for the Visual Studio family.

[See here for documentation](https://docs.microsoft.com/en-us/dotnet/framework/mef/).

### Part

An object exported to MEF through the `Export` attribute. Parts can be considered as **components** that are managed by MEF.
