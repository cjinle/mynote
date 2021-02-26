# C# 导入dll

## 安装.net


## 添加nuget源
```bat
dotnet nuget add https://api.nuget.org/v3/index.json
dotnet nuget list source
```

## 安装dll
```bat
cd <project-dir>
dotnet add package Newtonsoft.Json --version 12.0.3
```