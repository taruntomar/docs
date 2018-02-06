    How it works?

nuget-repo has three sub folder

 .\source | It contains all packages in extracted form, this is the folder which you need to specity in nuget install -source 
 .\reserves   | It contains only *.nupkg, this is required to initialize a new nuget repository. ex. nuget init
 .\libs     | It contains final output of nuget install -outputDir .\libs . This is the directory to which a project can directly refer to 
 
 .\NuGet.exe - the latest version of nuget.exe
 .\NuGet.config - the configuration of Nuget.exe
 
 ******************
 Powershell extension (Must if you are going to have other than .net core projects)
  > open powershell (Run as Admin)
  > Install-PackageProvider Nuget –force –verbose
  > Install-Module –Name PowerShellGet –Force –Verbose
  > exit and restart PowerShell
 ******************

 load this commandlet (not required in all cases)
 Import-Module .\NuGet.PackageManagement.PowerShellCmdlets.dll

 Some Example Commands:
 
****************
 Sample NuGet.config
****************
 <?xml version="1.0" encoding="utf-8"?>
<configuration>
  <packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />
    <add key="local" value="D:\Notifier\dotnet\NuGet-Repo" protocolVersion="3" />
  </packageSources>
  <disabledPackageSources>
    <add key="Microsoft and .NET" value="true" />
  </disabledPackageSources>
</configuration>

*******************

