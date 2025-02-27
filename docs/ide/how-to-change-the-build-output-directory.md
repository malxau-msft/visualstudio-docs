---
title: 'Change the build output directory'
description: Specify the location of output generated by your project on a per-configuration basis (for debug, release, or both) in Visual Studio.
ms.date: 08/14/2023
ms.subservice: compile-build
ms.topic: how-to
helpviewer_keywords:
- output directory, changing
author: ghogen
ms.author: ghogen
manager: jmartens
---
# Change the build output directory

You can specify the location of output generated by your project on a per-configuration basis (for debug, release, or both).

:::moniker range="vs-2019"
## Change the build output directory

1. To open the project's property pages, right-click on the project node in **Solution Explorer** and select **Properties**.

2. Select the appropriate tab based on your project type:

   - For C#, select the **Build** tab.
   - For Visual Basic, select the **Compile** tab.
   - For C++ or JavaScript, select the **General** tab.

3. In the configuration drop-down at the top, choose the configuration whose output file location you want to change (**Debug**, **Release**, or **All Configurations**).

4. Find the output path entry on the page&mdash;it differs depending on your project type:

   - **Output path** for C# and JavaScript projects
   - **Build output path** for Visual Basic projects
   - **Output directory** for Visual C++ projects

   Type in the path to generate output to (absolute, or relative to the root project directory), or choose **Browse** to browse to that folder.

   ![Output path property for a Visual Studio C# project](media/output-path.png)
   
   > [!NOTE]
   > Some projects will by default include framework and runtime in the build path. To change this, right-click the project node in **Solution Explorer**, select **Edit Project File**, and add the following:

   > ```xml
   > <PropertyGroup>
   >   <AppendTargetFrameworkToOutputPath>false</AppendTargetFrameworkToOutputPath>
   >   <AppendRuntimeIdentifierToOutputPath>false</AppendRuntimeIdentifierToOutputPath>
   > </PropertyGroup>
   > ```

> [!TIP]
> If the output is not being generated to the location that you specified, make sure you're building the corresponding configuration (for example, **Debug** or **Release**) by selecting it on the menu bar of Visual Studio.
>
> ![Build configuration picker in Visual Studio 2019.](media/build-configuration-chooser.png)

:::moniker-end

:::moniker range=">=vs-2022"
## Change the build output directory

In Visual Studio 2022, there are different Project Designer user interfaces, depending on your project type. C# .NET Framework and all Visual Basic projects use the legacy .NET Project Designer, but C# .NET Core (and .NET 5 and later) projects use the current .NET Project Designer. C++ projects use their own property pages user interface. The steps in this section depend on what Project Designer you're using.

### To change the build output directory using the legacy .NET Project Designer or C++ property pages

1. Right-click on the project node in **Solution Explorer** and select **Properties**.

1. Select the appropriate tab based on your project type:

   - For C#, select the **Build** tab.
   - For Visual Basic, select the **Compile** tab.
   - For C++ or JavaScript, select the **General** tab.

1. In the configuration drop-down at the top, choose the configuration whose output file location you want to change (**Debug**, **Release**, or **All Configurations**).

1. Find the output path entry on the page&mdash;it differs depending on your project type:

   - **Output path** for C# and JavaScript projects
   - **Build output path** for Visual Basic projects
   - **Output directory** for Visual C++ projects

   Type in the path to generate output to (absolute or relative to the root project directory), or choose **Browse** to browse to that folder instead.

   ![Output path property for a C# .NET Framework project](media/output-path.png)

   > [!NOTE]
   > Some projects will by default include framework and runtime in the build path. To change this, right-click the project node in **Solution Explorer**, select **Edit Project File**, and add the following:

   > ```xml
   > <PropertyGroup>
   >   <AppendTargetFrameworkToOutputPath>false</AppendTargetFrameworkToOutputPath>
   >   <AppendRuntimeIdentifierToOutputPath>false</AppendRuntimeIdentifierToOutputPath>
   > </PropertyGroup>
   > ```

### To change the build output directory using the current .NET Project Designer

1. Right-click on the project node in **Solution Explorer** and select **Properties**.

1. Expand the **Build** section, and select the **Output** subsection.

1. Find the **Base output path** for C#, and type in the path to generate output to (absolute or relative to the root project directory), or choose **Browse** to browse to that folder instead. Note that the configuration name is appended to the base output path to generate the actual output path.

   ![Output path property for a .NET Core C# project](media/vs-2022/output-path.png)

   > [!NOTE]
   > Some projects will by default include framework and runtime in the build path. To change this, right-click the project node in **Solution Explorer**, select **Edit Project File**, and add the following:

   > ```xml
   > <PropertyGroup>
   >   <AppendTargetFrameworkToOutputPath>false</AppendTargetFrameworkToOutputPath>
   >   <AppendRuntimeIdentifierToOutputPath>false</AppendRuntimeIdentifierToOutputPath>
   > </PropertyGroup>
   > ```

> [!TIP]
> If the output is not being generated to the location that you specified, make sure you're building the corresponding configuration (for example, **Debug** or **Release**) by selecting it on the menu bar of Visual Studio.
>
> ![Build configuration picker in Visual Studio 2022.](media/vs-2022/build-configuration-chooser.png)
:::moniker-end

## Build to a common output directory

By default, Visual Studio builds each project in a solution in its own folder inside the solution. You can change the build output paths of your projects to force all outputs to be placed in the same folder.

### To place all solution outputs in a common directory

1. Click on one project in the solution.

2. On the **Project** menu, click **Properties**.

3. In each project, depending on its type, select either **Compile** or **Build**, and set the **Output path** or **Base output path** to a folder to use for all projects in the solution.

4. Open the project file for the project, and add the following property declaration to the first property group.

   ```xml
   <PropertyGroup>
     <!-- existing property declarations are here -->
     <UseCommonOutputDirectory>true</UseCommonOutputDirectory>
   </PropertyGroup>
   ```

   Setting `UseCommonOutputDirectory` to `true` tells Visual Studio and its underlying build engine (MSBuild) that you're putting multiple project outputs in the same folder, and so MSBuild omits the copying step that normally happens when projects depend on other projects.

5. Repeat steps 1-4 for all projects in the solution. You can skip some projects if you have some exceptional projects that should not use the common output directory.

### To set the intermediate output directory for a project (.NET projects)

1. Open the project file.

1. Add the following property declaration to the first property group.

   ```xml
   <PropertyGroup>
     <!-- existing property declarations are here -->
     <IntermediateOutputPath>path</IntermediateOutputPath>
   </PropertyGroup>
   ```

   The path is relative to the project file, or you can use an absolute path. If you want to put the project name in the path, you can reference it by using the MSBuild properties `$(MSBuildProjectName)`, `$(MSBuildProjectDirectory)`. For more properties you can use, see [MSBuild reserved and well-known properties](../msbuild/msbuild-reserved-and-well-known-properties.md).

1. Visual Studio still creates the obj folder under the project folder when you build, but it's empty. You can delete it as part of the build process. One way to do that is to add a post-build event to run the following command:

   ```cmd
   rd "$(ProjectDir)obj" /s /q
   ```

   See [Specify custom build events](specifying-custom-build-events-in-visual-studio.md).

## Related content

- [Build page, Project Designer (C#)](../ide/reference/build-page-project-designer-csharp.md)
- [General Property page (project)](/cpp/build/reference/general-property-page-project)
- [Compile and build](../ide/compiling-and-building-in-visual-studio.md)
