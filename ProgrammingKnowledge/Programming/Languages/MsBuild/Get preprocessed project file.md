MSBuild bietet eine Möglichkeit das komplette CsProj File (inklusive aller automatisch inkludierter props- und target-Files) in ein File umzuleiten, und zwar mit dem [preprocess](https://learn.microsoft.com/en-us/visualstudio/msbuild/msbuild-command-line-reference?view=vs-2022#preprocess)-switch. Der Switch wird auch von [[DotNet]] build supported.

```
dotnet build -pp:out.txt your.csproj

```

#MSBuild 
#dotnetbuild
