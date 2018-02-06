
SET currentPath=%~dp0
SET repoPath=%currentPath%..\..\NuGet-Repo\
SET notifierPath=%currentPath%..\..\Notifier\
SET examplePath=%currentPath%..\..\Examples\

dotnet restore %notifierPath%\src\ -s %repoPath%

Rem | Compiles the application, reads through its dependencies specified in the project file, and 
Rem | publishes the resulting set of files to the build\release directory.
Rem | dotnet publish ..\Notifier.csproj --configuration Release --output .\build\release
Rem | Pack output into nugetpackage

Rem | - verbosity level q[uiet], m[inimal], n[ormal], d[etailed], and diag[nostic]

dotnet clean %notifierPath%\src\Notifier.csproj --configuration Release --output %notifierPath%\build\release -v n


dotnet pack %notifierPath%\src\Notifier.csproj --configuration Release --output %notifierPath%\build\release --version-suffix rel /p:PackageVersion=1.0.0 -v n

Rem | copy to local repository

Start %repoPath%\nuget.exe init %notifierPath%\build\release\ %repoPath% 


Rem publish this nuget to central repository of mdt



