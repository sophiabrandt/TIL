# Use the dotnet CLI

Create a new solution:

```sh
dotnet new sln -n <solution name>
# `dotnet new sln` creates a new .sln file in the current dir with the same name
# as theFolder
```

List all available templates to create a new project:

```sh
dotnet new list
```

Create a new project:

```sh
dotnet new webapi -o <output-dir>
```

Add the project to the solution:

```sh
dotnet sln add <project name>
```

Navigate to the project folder and add a nuget package:

```sh
dotnet add package <full name of the package>
```

Add a reference

```sh
dotnet add <source project.csproj> reference <target project.csproj>
```
