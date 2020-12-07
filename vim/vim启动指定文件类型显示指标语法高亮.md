# vim启动指定文件类型显示指标语法高亮

vim启动指定文件类型显示指标语法高亮

```sh
au BufNewFile,BufRead *.pl setf plsql
```

上面的配置意思是，打开`.pl`结尾的文件，
以`plsql`语法高这来显示文件。