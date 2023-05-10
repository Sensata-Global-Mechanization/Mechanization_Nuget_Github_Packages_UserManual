# Create and Package nuget package for Dot Net Core or DotNet Standard projects

#### In this manual, we will use a `nuget.config` file to store configuration values for packaging and publishing .NET Core or .NET Standard NuGet packages to your organization's GitHub Packages. Additionally, the NuGet Package Manager will be used to install the packages in a new project.

### Prerequisites
1. Visual Studio 2022 with .NET Core or .NET Standard support.
2. A GitHub account with access to your organization's repositories.
3. A Personal Access Token (PAT) at organization level with `read:packages` and `write:packages` scopes.
Create a nuget.config file for your project
1.	Open your project or solution in Visual Studio.
2.	Select `Tools` > `NuGet Package Manager` > `Package Manager Console` to open the Package Manager Console window.
3.	In the console, use the `pwd` command to print the current working directory. For example:
```bash
PM> pwd

Path
----
C:\Users\YourUsername
```

4.	Use the `cd` command to navigate to the directory where you want to create the `nuget.config` file. For example, if you want to create the file in the root of your project repository, navigate to that directory:

```bash
PM> cd C:\Path\To\Your\Project\Repository
```

5.	Once you are in the desired directory, run the command `dotnet new nugetconfig`. This will create a new `nuget.config` file in the current directory:

```bash
PM> dotnet new nugetconfig
The template "NuGet Config" was created successfully.
```


6.	In your .NET Core or .NET Standard project folder, Edit the `nuget.config` with the content in the Sample nuget.config file.–
 
```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <packageSources>
    <clear />
    <add key="github" value="https://nuget.pkg.github.com/Sensata-Global-Mechanization/index.json" />
  </packageSources>
  <packageSourceCredentials>
    <github>
      <add key="Username" value="YOUR_GITHUB_USERNAME" />
      <add key="ClearTextPassword" value="ghp_SampleAPIKEY" />
    </github>
  </packageSourceCredentials>
</configuration>
```
 
7.	Replace `Sensata-Global-Mechanization` with another GitHub organization's name, `YOUR_GITHUB_USERNAME` with your GitHub username, and `ghp_SampleAPIKEY` with the Personal Access Token you created earlier.
8.	Save and close the `nuget.config` file.


### Configure your project for NuGet packaging
1.	Open your .NET Core or .NET Standard project in Visual Studio 2022.
2.	Right-click the project in the Solution Explorer and click 'Properties'.
3.	In the 'Properties' window, select the 'Package' tab.

![](Package1.png)

![](Package2.png)

4.	Fill in the required fields, such as Package ID, Version, Authors, and Description.

 ![](Package3.png)

5.	Check the 'Generate NuGet package on build' option.
6.	Save the changes and close the 'Properties' window.


### Build your project and generate the NuGet package

1.	Right-click the project in the Solution Explorer and click 'Rebuild'. This will build your project and generate a NuGet package in the output folder (usually in the "bin\Release" or "bin\Debug" folder).
2.	Locate the generated .nupkg file in the output folder.

![](Package4.png)

### Publish your NuGet package to GitHub Packages using Package Manager Console
1.	In Visual Studio 2022, open the Package Manager Console by clicking 'View' > 'Other Windows' > 'Package Manager Console'.
2.	In the Package Manager Console, navigate to the folder containing the .nupkg file by running the command:

```bash
cd "path\to\your\output\folder"
```

2.	Run the following command to publish the NuGet package to GitHub Packages:

```bash
nuget push -Source "GitHub" -ApiKey az YOUR_PACKAGE.nupkg
```


3.	Replace `YOUR_PACKAGE.nupkg` with the filename of the .nupkg file generated earlier.
4.	The NuGet package should now be published to your organization's GitHub Packages. You can verify this by visiting the 'Packages' tab in your GitHub organization's profile.






### Use NuGet Package Manager to install packages from GitHub Packages in a new project

1.	Open the new project in Visual Studio 2022 that needs to consume the published NuGet package.
2.	Right-click on the project in the Solution Explorer and click 'Add' > 'New Item'.
3.	In the 'Add New Item' dialog, search for 'NuGet' and select 'NuGet Configuration File'.
4.	Click 'Add' to create a new `nuget.config` file.
5.	Open the `nuget.config` file and add the following content:

```xml
xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
<packageSources>
<add key="GitHub" value="https://nuget.pkg.github.com/ORGANIZATION_NAME/index.json" />
</packageSources>
<packageSourceCredentials>
<GitHub>
<add key="Username" value="YOUR_GITHUB_USERNAME" />
<add key="ClearTextPassword" value="YOUR_PERSONAL_ACCESS_TOKEN" />
</GitHub>
</packageSourceCredentials>
</configuration>
```
* Replace `ORGANIZATION_NAME` with your GitHub organization's name, `YOUR_GITHUB_USERNAME` with your GitHub username, and `YOUR_PERSONAL_ACCESS_TOKEN` with the Personal Access Token you created earlier. 

6.	Save and close the `nuget.config` file.
7.	In Visual Studio, right-click on the project in the Solution Explorer and click 'Manage NuGet Packages'.
 
![](Picture4.1.png)

![](Package5.png)

![](Package6.png)
 
8.	In the 'NuGet Package Manager' window, click on the 'Settings' (gear) icon in the top right corner.
9.	In the 'Options' window, under 'NuGet Package Manager' > 'Package Sources', make sure the GitHub source is added and enabled. If it's not, add a new package source with the name 'GitHub' and the source URL `https://nuget.pkg.github.com/ORGANIZATION_NAME/index.json`, then click 'Update' and 'OK'.
10.	Back in the 'NuGet Package Manager' window, select the 'GitHub' package source from the drop-down menu.
11.	Search for your package using the Package ID you specified when publishing.
12.	Select your package from the search results and click 'Install' to add it to your project.



# Dot Net Framework Projects Instructions - Package and Publish NuGet Packages for .NET Framework Projects

### This manual provides step-by-step instructions for creating, packaging, and publishing NuGet packages for .NET Framework projects using the Package Manager Console in Visual Studio.

Resource -  [Quickstart: Create and publish a package using Visual Studio (.NET Framework, Windows) | Microsoft Learn](https://learn.microsoft.com/en-us/nuget/quickstart/create-and-publish-a-package-using-visual-studio-net-framework)

### Prerequisites
1.	Visual Studio with .NET Framework support.
2.	NuGet CLI installed. You can download it from [here](https://www.nuget.org/downloads).
3.	A GitHub account with access to your organization's repositories.
4.	A Personal Access Token (PAT) with `read:packages` and `write:packages` scopes.
*   [Creating a personal access token - GitHub Docs](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token) 

### Create a NuGet Specification file

1.	Open the Package Manager Console in Visual Studio by clicking 'View' > 'Other Windows' > 'Package Manager Console'.
2.	In the Package Manager Console, run the following command:

```bash
nuget spec
```
* This command creates a `.nuspec` file in your project folder. 

```xml
<?xml version="1.0" encoding="utf-8"?>
<package >
  <metadata>
    <id>SensataUILib</id>
    <version>1.0.0</version>
    <title>SensataUILib</title>
    <authors>jmarioiii</authors>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <license type="expression">MIT</license>
    <!-- <icon>icon.png</icon> -->
    <projectUrl>https://github.com/Sensata-Global-Mechanization/Sand-Box-.NET-Modular-UI-Library</projectUrl>
    <description>Repository for the modular .NET UI library</description>
    <releaseNotes>First NuGet Package for SensataUILibrary</releaseNotes>
    <copyright>Copyright 2023</copyright>
    <tags>SensataModularUILibrary MechanizationUILibrary</tags>
  </metadata>
</package>
```

 
### Edit the .nuspec file
1.	Open the generated `.nuspec` file in Visual Studio or any text editor.
2.	Edit the file according to your package requirements. Here is a sample `.nuspec` file:

```xml
<?xml version="1.0"?>
<package>
<metadata>
<id>MyPackageId</id>
<version>1.0.0</version>
<title>My Package Title</title>
<authors>Your Name</authors>
<owners>Your Name</owners>
<requireLicenseAcceptance>false</requireLicenseAcceptance>
<description>A brief description of your package.</description>
<releaseNotes>Summary of changes made in this release of the package.</releaseNotes>
<copyright>Copyright 2022 Your Name</copyright>
<tags>tag1 tag2 tag3</tags>
</metadata>
</package>
```
 
 ![](Picture7.png)
 
* Replace the placeholder values with your package's specific details. 
3. Save and close the `.nuspec` file.

### Package the NuGet package

1.	In the Package Manager Console, navigate to the folder containing the `.nuspec` file by running the command:
```bash
cd "path\to\your\project\folder"
```
2.	Run the following command to create the NuGet package based on the `.nuspec` file:
```bash
nuget pack YourPackageName.nuspec
```
* Replace `YourPackageName.nuspec` with the name of your `.nuspec` file. This command creates a `.nupkg` file in the project folder.

### Publish the NuGet package to GitHub Packages

1. In the Package Manager Console, run the following command to publish the NuGet package to your organization's GitHub Packages:
```bash
dotnet nuget push SensataUILib.1.0.0.nupkg -k YOUR_PERSONAL_ACCESS_TOKEN -s https://nuget.pkg.github.com/Sensata-Global-Mechanization/index.json
```
* Replace `SensataUILib.1.0.0.nupkg` with the name of your `.nupkg` file, `YOUR_PERSONAL_ACCESS_TOKEN` with the Personal Access Token you created earlier
2. The NuGet package should have now been published to your organization's GitHub Packages.