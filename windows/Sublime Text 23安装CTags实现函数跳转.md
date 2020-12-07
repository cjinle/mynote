# Sublime Text 2/3安装CTags实现函数跳转

### 安装Sumlime Text
略

### 安装ctags
下载`ctags`程序，放到目录D:/ctags/下

### 安装ctags插件
1. 打开Sublime Text
2. `Preferences->Package Control->Install Package->CTags`
3. 配置ctags插件
4. `Preferences->Package Settings->CTags->Settings - User`，复制下面的配置
```json
{
    "command": "d:/ctags/ctags.exe"
}
```
5. 在项目生成ctags索引，在左侧项目目录下，CTags:Rebuild Tags，然后在函数名上，右键Navigate To Definition就可以实现跳转了
6. 实现用Ctrl+鼠标左键跳转。`Preferences->Package Settings->CTags->Mouse Binding - User`，复制下面的配置
```json
[
	{
		"button": "button1",
		"count": 1,
		"press_command": "drag_select",
		"modifiers": ["ctrl"],
		"command": "navigate_to_definition"
	}
]
```
记录两个常的快捷键配置
```json
{ "keys": ["ctrl+d"], "command": "run_macro_file", "args": {"file": "Packages/Default/Delete Line.sublime-macro"} },
{ "keys": ["ctrl+l"], "command": "duplicate_line" }
```