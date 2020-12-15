# golang的vscode设置

## settings.json
```js
{
	"go.formatTool": "gofmt",
    "go.useLanguageServer": true,
    "[go]":{
        "editor.insertSpaces": false,
        "editor.formatOnSave": true,
        "editor.codeActionsOnSave": {
            "source.organizeImports": true
        }
    }
}
```

## VS Code中如何关闭保存Go语言文件时自动去除未引用包的行为

在VS Code中的Preference的Settings中搜索goimports，会看到`Go: Format Tool`一项，将使用的`goreturns`或`goimports`换成`gofmt`即可。

因为`goreturns`或`goimports`都会自动做自动包导入或者将未引用的包去除的工作。当然，这样设置了之后，使用到了但却没有导入（import）的包一定要记得自己手动确保导入。方便性两者不可兼得。

## VSCode golang 提示太慢

go的自动补全靠的时gocode,我们可以gocode -debug查看偏移，自动补全正常时偏移小于1ms,设置为on时偏移有3秒
```
gocode -debug
```

###  解决方法
```
cp -rf $GOPATH/bin/gocode.exe $GOPATH/gocode.exe
```