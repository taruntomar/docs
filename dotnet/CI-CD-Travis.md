variables:
{solution_name}
{project_name}
{assembly_name}
{description_about_library}

# Setup CI/CD using GitHub and TravisCI

## Prepare NuGET for continuous deployment

1. Goto https://www.nuget.org/ and signin using microsoft account.
2. goto API Keys, create a key, copy this key in a text file, save.

------------------------------------------------------------------

## Create a dll Project

1. Create a dll (.Net Framework project) and host it in GitHub.
2. create a file named {project_name}.nuspec in project and add the following content in it.

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
    <!-- Required elements-->
    <id>{project_name}</id>
    <version>1.0.0</version>
    <description>{description_about_library}</description>
    <authors>{author_name}</authors>

    <!-- Optional elements -->
    <dependencies>
        <dependency id="{dependent_package_name}" version="{version}" />
    </dependencies>

    </metadata>
    <!-- Optional 'files' node -->
    <files>
     <file src="bin/Release/{assembly_name}.dll" target="lib/net45" />
    </files>
</package>
```

-----------------------------------------------------------------

## Setup travis for continuous integration 

1. Goto https://travis-ci.org/ and register
2. goto your profile and add newly created project repository.
3. come back to HomePage > More Options > Settings
4. create below three varibles 
    * MAJOR_VERSION_NUMBER :1
    * MINOR_VERSION_NUMBER :0
    * NUGET_API_KEY: paste the newly created key from https://www.nuget.org/

5. Add a file in solution with name '.travis.yml' using visual studio.
    add the below content to the file.

```yml
    language: csharp
solution: {solution_name}.sln
install:
  - curl -L -o nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
  - mono nuget.exe restore {solution_name}.sln
# - mono nuget.exe install NUnit.Runners -Version 3.6.1 -OutputDirectory testrunner
script:
  - xbuild /p:Configuration=Release {solution_name}.sln
#  - mono ./testrunner/NUnit.ConsoleRunner.3.6.1/tools/nunit3-console.exe ./<Project Name>Test/bin/Release/<Project Name>Test.dll
  - mono nuget.exe pack ./{project_name}/{project_name}.nuspec -Version $MAJOR_VERSION_NUMBER.$MINOR_VERSION_NUMBER.$TRAVIS_BUILD_NUMBER
  - mono nuget.exe setApiKey $NUGET_API_KEY -Source https://www.nuget.org -Verbosity quiet
  - mono nuget.exe push {assembly_name}.$MAJOR_VERSION_NUMBER.$MINOR_VERSION_NUMBER.$TRAVIS_BUILD_NUMBER.nupkg -Source https://www.nuget.org/api/v2/package  
```

> Make a commit and check whether build has started or not on Travis-CI.
