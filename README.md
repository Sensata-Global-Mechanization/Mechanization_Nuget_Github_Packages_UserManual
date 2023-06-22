# Create and Package NuGet package for Dot Net Core or DotNet Standard projects

#### In this manual, we will use a `nuget.config` file to store configuration values for packaging and publishing .NET Core or .NET Standard NuGet packages to your organization's GitHub Packages. Additionally, the NuGet Package Manager will be used to install the packages in a new project

Resource -  [Quickstart: Create and publish a package using Visual Studio (.NET Core and Standard, Windows) | Microsoft Learn](https://learn.microsoft.com/en-us/nuget/quickstart/create-and-publish-a-package-using-visual-studio?tabs=netcore-cli)

### Prerequisites

1. Visual Studio 2022 with .NET Core or .NET Standard support.
2. A GitHub account with access to your organization's repositories.
3. A Personal Access Token (PAT) at organization level with `read:packages` and `write:packages` scopes.

### Create a Personal Access Token at the organization level with read:packages and write:packages scopes for Github

1. Go to your GitHub account settings.
2. Select Developer settings.
3. Select Personal access tokens.
4. Click on Generate new token.
5. Give your token a descriptive name.
6. Select the read:packages and write:packages scopes for this token to authorize for your specific tasks.

* a member of a GitHub organization can use a personal access token with the `read:packages` and `write:packages` scopes to publish packages to GitHub Packages within the organization.

7. Set the expiration date for your token to a `SEPCIFIC DATE` rather than `never` if you don’t want it to expire to soon enough.

* setting the expiration date to `never` ensures that the token does not expire, it is generally recommended to set an expiration date for `security reasons`

8. Click on Generate token.

### Create a nuget.config file for your project

1. Open your project or solution in Visual Studio.
2. Select `Tools` > `NuGet Package Manager` > `Package Manager Console` to open the Package Manager Console window.
3. In the console, use the `pwd` command to print the current working directory. For example:

```bash
PM> pwd

Path
----
C:\Users\YourUsername
```

4. Use the `cd` command to navigate to the directory where you want to create the `nuget.config` file. For example, if you want to create the file in the root of your project repository, navigate to that directory:

```bash
PM> cd C:\Path\To\Your\Project\Repository
```

5. Once you are in the desired directory, run the command `dotnet new nugetconfig`. This will create a new `nuget.config` file in the current directory:

```bash
PM> dotnet new nugetconfig
The template "NuGet Config" was created successfully.
```

6. In your .NET Core or .NET Standard project folder, Edit the `nuget.config` with the content in the Sample nuget.config file.–

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

7. Replace `Sensata-Global-Mechanization` with another GitHub organization's name, `YOUR_GITHUB_USERNAME` with your GitHub username, and `ghp_SampleAPIKEY` with the Personal Access Token you created earlier.
8. Save and close the `nuget.config` file.

### Configure your project for NuGet packaging

1. Open your .NET Core or .NET Standard project in Visual Studio 2022.
2. Right-click the project in the Solution Explorer and click 'Properties'.
3. In the 'Properties' window, select the 'Package' tab.

![](Package1.png)

![](Package2.png)

4. Fill in the required fields, such as Package ID, Version, Authors, and Description.

 ![](Package3.png)

5. Check the 'Generate NuGet package on build' option.
6. Save the changes and close the 'Properties' window.

### Build your project and generate the NuGet package

1. Right-click the project in the Solution Explorer and click 'Rebuild'. This will build your project and generate a NuGet package in the output folder (usually in the "bin\Release" or "bin\Debug" folder).
2. Locate the generated .nupkg file in the output folder.

![](Package4.png)

### Publish your NuGet package to GitHub Packages using Package Manager Console

1. In Visual Studio 2022, open the Package Manager Console by clicking 'View' > 'Other Windows' > 'Package Manager Console'.
2. In the Package Manager Console, navigate to the folder containing the .nupkg file by running the command:

```bash
cd "path\to\your\output\folder"
```

2. Run the following command to publish the NuGet package to GitHub Packages:

```bash
nuget push -Source "GitHub" -ApiKey az YOUR_PACKAGE.nupkg
```

3. Replace `YOUR_PACKAGE.nupkg` with the filename of the .nupkg file generated earlier.
4. The NuGet package should now be published to your organization's GitHub Packages. You can verify this by visiting the 'Packages' tab in your GitHub organization's profile.

### Use NuGet Package Manager to install packages from GitHub Packages in a new project

1. Open the new project in Visual Studio 2022 that needs to consume the published NuGet package.
2. Right-click on the project in the Solution Explorer and click 'Add' > 'New Item'.
3. In the 'Add New Item' dialog, search for 'NuGet' and select 'NuGet Configuration File'.
4. Click 'Add' to create a new `nuget.config` file.
5. Open the `nuget.config` file and add the following content:

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

6. Save and close the `nuget.config` file.
7. In Visual Studio, right-click on the project in the Solution Explorer and click 'Manage NuGet Packages'.

![](Picture4.1.png)

![](Package5.png)

![](Package6.png)

8. In the 'NuGet Package Manager' window, click on the 'Settings' (gear) icon in the top right corner.
9. In the 'Options' window, under 'NuGet Package Manager' > 'Package Sources', make sure the GitHub source is added and enabled. If it's not, add a new package source with the name 'GitHub' and the source URL `https://nuget.pkg.github.com/ORGANIZATION_NAME/index.json`, then click 'Update' and 'OK'.
10. Back in the 'NuGet Package Manager' window, select the 'GitHub' package source from the drop-down menu.
11. Search for your package using the Package ID you specified when publishing.
12. Select your package from the search results and click 'Install' to add it to your project.

# Dot Net Framework Projects Instructions - Package and Publish NuGet Packages for .NET Framework Projects

#### Below is step-by-step instructions for creating, packaging, and publishing NuGet packages for .NET Framework projects using the Package Manager Console in Visual Studio

Resource -  [Quickstart: Create and publish a package using Visual Studio (.NET Framework, Windows) | Microsoft Learn](https://learn.microsoft.com/en-us/nuget/quickstart/create-and-publish-a-package-using-visual-studio-net-framework)

### Prerequisites

1. Visual Studio with .NET Framework support.
2. NuGet CLI installed. You can download it from [here](https://www.nuget.org/downloads).
3. A GitHub account with access to your organization's repositories.
4. A Personal Access Token (PAT) with `read:packages` and `write:packages` scopes.

* [Creating a personal access token - GitHub Docs](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token)

### Create a NuGet Specification file

1. Open the Package Manager Console in Visual Studio by clicking 'View' > 'Other Windows' > 'Package Manager Console'.
2. In the Package Manager Console, run the following command:

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

1. Open the generated `.nuspec` file in Visual Studio or any text editor.
2. Edit the file according to your package requirements. Here is a sample `.nuspec` file:

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

1. In the Package Manager Console, navigate to the folder containing the `.nuspec` file by running the command:

```bash
cd "path\to\your\project\folder"
```

2. Run the following command to create the NuGet package based on the `.nuspec` file:

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

# Automated Publishing of Nuget Packages to GitHub Packages

* Make sure a library project has it's own independent git repository.

* Setup .github/workflows/ folder structure on the git repository root level folder.

* Good to Read Links about Github packages and automated publishing -
  * Link 1 -
  * Link 2 -

* Create a file with format .yml extension in the workflows folder.

* Regarding the .yml file, I gave an example below which is part of all the Mechanization dot net library repositoriess.

```bash
# This is the name of your workflow
name: Build .NET Library

# This workflow is triggered on push to the main branch
on:
  push:
    branches:
      - main

# Jobs to be executed in this workflow
jobs:
  # This job is named "build"
  build:
    # This job will be run on the latest version of windows
    runs-on: windows-latest

    # Steps the job will take
    steps:
    # This step checks out a copy of your repository
    - name: Checkout repository
      uses: actions/checkout@v3.5.0

    # This step sets up .NET on the runner
    - name: Setup .NET
      uses: actions/setup-dotnet@v3.0.3
      with:
        dotnet-version: '6.0' # This specifies the .NET version to be used
    
    # This step adds a GitHub package source for NuGet packages
    - name: Add GitHub Package Source
      run: |
        dotnet nuget add source https://nuget.pkg.github.com/Sensata-Global-Mechanization/index.json --name github --username ${{ secrets.SECRET_NAME }} --password ${{ secrets.GH_PACKAGES_TOKEN }} --store-password-in-clear-text
      shell: pwsh
      
    # This step restores any dependencies and installs the M2MqttDotnetCore package
    - name: Restore and install dependencies
      run: |
        dotnet restore
        dotnet add package M2MqttDotnetCore --version 1.1.0

    # This step builds the .NET application in Release mode
    - name: Build
      run: dotnet build --configuration Release --no-restore

    # This step runs tests on the built application
    - name: Test
      run: dotnet test --no-restore --verbosity normal
      
    # This step lists the contents of the artifacts directory
    - name: List artifacts directory
      run: |
        ls bin/Release
    
    # This step publishes the built package to GitHub Packages
    - name: Publish to GitHub Packages
      run: |
        $githubSourceExists = (dotnet nuget list source | Select-String -Pattern "github")
        if (-not $githubSourceExists) 
        {
            dotnet nuget add source https://nuget.pkg.github.com/Sensata-Global-Mechanization/index.json --name github --username ${{ secrets.SECRET_NAME }} --password ${{ secrets.GH_PACKAGES_TOKEN }} --store-password-in-clear-text
        }
        $packages = Get-ChildItem -Path ./bin/Release -Filter *.nupkg -Recurse
        if ($packages) 
        {
            foreach ($package in $packages)
            {
                Write-Output "Found package $($package.Name)"
                dotnet nuget push "$($package.FullName)" --source github
            }
        }
        else 
        {
            Write-Error "No package files found in the artifacts directory."
        }
      shell: pwsh

    # This step uploads the artifacts to GitHub
    - name: Upload artifacts
      uses: actions/upload-artifact@v2
      with:
        name: library-artifacts
        path: ./artifacts/

```

* The above example script will setup the dot net environment for build, package and publish of the nuget package to github packages on every time a branch is merged into main.

* Source - [Sensata Global Mechanization Nuget Package Source URL](https://nuget.pkg.github.com/Sensata-Global-Mechanization/index.json) is the source for Sensata Global Mechanization packages.
* secrets.SECRET_NAME - This is to make sure no hard coding of username is done in the script
* secrets.GH_PACKAGES_TOKEN - This is to make sure no hard coding of password is done in the script
* The secrets are stored in repository settings like shown in the image below. For now every library repository is setup with secrets corresponding to satya or myself. We created a PAT token with necessary permissions like read:write repositories, read:write packages.

    ![Github Secrets](SecretsGithub.png)

* The Action is executed once the branch is requested to merge into main and the corresponding pull request is approved and merge pull request button is cliked.

* The below images show the actions tab in the repository and the corresponding actions executed for the merge pull request.
    ![GitHub Actions Window 1](ActionsGithub.jpeg)

    ![GitHub Actions Window 2](ActionsGithub2.jpeg)

    ![GitHub Actions Window 3](ActionsGitHub3.png)

* The below image shows the packages tab in the repository and the corresponding packages published to github packages.

    ![Alt text](GitHubNugetPackages.png)

* The below image shows the specific details of the package published to github packages.

    ![Alt text](GitHubNugetPackagesDetails.png)

* The current CI scripts are run directly on Github Enterprise Cloud. We can also setup a self hosted runner on a local machine and run the CI scripts on the local machine. This is useful when we want to run the CI scripts on a local machine and publish the packages to a Github nuget packages server.

* We have a limit of 50000 minutes in Sensata Global Mechanization Github Organization per month. At current levels we might not reach the limit. But during first few months we will keep monitoring and we can setup a self hosted runner on a local machine and run the CI scripts on the local machine and publish the packages to a Github nuget packages server.

* CI scripts can also be used to perform unit testings on our repositories. Team members can explore and come up with suggestions as we progress further.

