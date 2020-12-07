# gVim设置字体(guifont)

经过多方试验，在win下设置vim的大小终于成功了，备份如下，
现在把gvim7.1更改字体的方法记录如下，一段时间后，可能会失效，对他人造成困扰吧？！^_^   在_vimrc中写： `set guifont=courier_new:h10`    //设置字体为Courier New,大小10号
若在linux下，应该写为，
`set guifont=courier_new\(空格)h10`
以下是网络上搜到的东东，以便日后参考：

在控制台下的VIM是不能够改变字体的，因为字体的改变是随着终端字体的变化而变化的，但是在GVIM中，你却有权力将字体改变成自己想要的样子。
在Linux下设置字体的命令是：
` : set guifont = Courier\   14 `
而在Windows下则是：
` : set guifont = Courier:h14 `
当然，如果需要设置多个字体，则我们可以在各个字体之间添加逗号(,)来设置多个字体，如：
`: set  guifont = Courier\ New\ 12 , Arial\ 10`

如果字体名字中含有空格，则我们需要将其使用\进行转义，而在windows下则可以将空格转换为:字符。当然，这样设置之后只会对当前会话有效，而如果想每次都使用的话，则需要将其加入到其gvimrc设置文件中(将命令中前面的:去掉)。
如果你不知道可用的字体名字，使用下面的命令可以得到一个字体名字的列表：

` :set guifont=*`

如果需要想对特定的文件类型使用特定的字体，则可以将下面的语句加入到vimrc文件中去：
` autocmd BufEnter  *. txt set guifont = Arial \ 12 `
这样，在下次打开.txt文件的时候，就会设置字体Arial 12字体。

需要注意的是，每次改变字体大小的时候，GVim会调整自己的窗口大小来适应字体的变化。

