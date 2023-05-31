
Mit Hilfe von [Directory.Packages.props](https://devblogs.microsoft.com/nuget/introducing-central-package-management/?WT.mc_id=DT-MVP-5004452)kann man NuGet Versionen zentral in einem File verwalten.

```
<Project>
  <PropertyGroup>
    <ManagePackageVersionsCentrally>true</ManagePackageVersionsCentrally>
  </PropertyGroup>
  <ItemGroup>
    <PackageVersion Include="Newtonsoft.Json" Version="13.0.1" />
  </ItemGroup>
</Project>
```


#NuGet 