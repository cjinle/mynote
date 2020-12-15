# vim直接改变源码文件类型高亮

在vim的命令模式下，比如你在修改一个普通的文件，没有高亮显示
但这时想显示的是MySQL的源码高亮，这时只需要输入下面命令即可

```
: set ft=mysql
: se ft=mysql
: set filetype=mysql
: set filetype=mysql
```

## 指定文件后缀高亮

```
au BufNewFile,BufRead *.pl setf plsql
```
上面的配置意思是，打开`.pl`结尾的文件，
以`plsql`语法高这来显示文件。

## go语言高亮

```
cp -rv /usr/local/go/misc/vim/* /usr/share/vim/vim70/
```

