# electron入门

[文档](http://electronjs.org/docs/all)

## 调试
 - 开发者工具
 - chrome inspect
 - vscode lanuch

## webContents
### 事件
 - did-finish-load
 - dom-ready

## process对象

`process.getCPUUsage`

`nodeIntegration`

##  file对象

阻止默认行为 `e.preventDefault()` 

### 事件
 - drop 
 - dragover

```js
dragWrapper.addEventListener("dragover", (e)=>{
  e.preventDefault()
})

// buffer --> string
const content = fs.readFileSync(path)
console.log(content.toString())
```

## webview对象 
允许webview展示，需要修改BrowserWindows的属性 `webviewTag: true`

### 事件
 - did-start-loading
 - did-stop-loading

```js
document.querySelector("#su").onclick = () => {
  alert("hello")
}
```

## window.open

## BrowserWindow

## BrowserView

## 对话框

## 系统快捷键

## 主进程与渲染进程通信

## 菜单

## 网络

## 集成vue

## 应用打包-vue

