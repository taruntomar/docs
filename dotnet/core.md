```
dotnet new console or dotnet new mvc
```
> dotnet core will create a new package cache, for offline use. mostly it will be in C:\Users\[username]\.nuget\packages
```
dotnet restore 
```
> this command will create two file under the folder obj, prop and target. the props file will contain the references to lib in offline cache, which will be require for compiling.
```
dotnet build
```
> this command will compile and build the project and put copy output in bin directory. it will also copy required dlls to bin.
```
dotnet add package [name]
```
 > this command will download package from online source to offline repository and add an entry in .csproj file