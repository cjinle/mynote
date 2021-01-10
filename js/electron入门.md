# electron入门

[文档](http://electronjs.org/docs/all)

main.js主进程，renderer.js渲染进程
如果在非主进程使用electron，需要使用的是`electron.remote`

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

```js
const subWin
function openNewWindow() {
  subWin = window.open('page.html', 'popup')
}

window.opener.postMessage("子窗口发来的信息")

window.addEventListener("message", (msg)=>{
  console.log("接收到的信息", msg)
})

function closeWindow() {
  subWin.close()
}
```

## BrowserWindow

### 事件
 - ready-to-show


```js
mainWindow.once("ready-to-show", ()=>{ // once只执行一次
  mainWindow.show()  
})
```

## BrowserView
和webview有点像

## 对话框

```js
const { dialog } = require('electron').remote

dialog.showOpenDialog({
  title: "选择文件",
  filters: [
    {name: "Custom File Type", extensions: ['js', 'html', 'json']}
  ]
}, result => {
  console.log(result)
})

dialog.showMessageBox({
  type: 'warning',
  title: '你确定吗？',
  message: '真的要删除这条数据吗？',
  buttons: ['OK', 'Cancel']
})

```

## 系统快捷键
```js
globalShortcut.register('CommandOrControl+X', () => { // 注册快捷键
  console.log('CommandOrControl+X is pressed')
})

globalShortcut.unregister('CommandOrControl+X') // 注销快捷键
globalShortcut.unregisterAll() // 注销所有快捷键
```

## 主进程与渲染进程通信

 - 主进程到渲染进程 `ipcMain`
 - 渲染进程到主进程 `ipcRenderer`

```js
// 主进程
const {ipcMain} = require('electron')
ipcMain.on("send-message-to-main-test", (event, args) => {
  event.reply("send-message-to-renderer-test", "来自主进程的消息")
})
mainWindow.webContents.send("send-message-to-renderer-test", "来自主进程主动发的消息")

// 渲染进程
const {ipcRenderer} = require('electron')
ipcRenderer.send("send-message-to-main-test", "来自渲染进程的消息666")

ipcRenderer.on("send-message-to-renderer-test", (event, args) => {
  console.log("渲染进程接收到的消息", args)
})
```

## 菜单

```js
const {Menu, MenuItem} = require('electron').remote
const template = [
  {label: "菜单一"},
  {label: "菜单二", click: ()=>{console.log("菜单二点击了")}},
  {role: "undo"},
  {type: "separator"},
  new MenuItem({label: "菜单三"}),
  submenu: [
    {label: "子菜单一"}
  ]
]
const menu = Menu.buildFromTemplate(template)
Menu.setApplicationMenu(menu)
menu.popup()
```

## 网络 net
类似node.js的http和https模块，但它使用的是Chromium原生网络库
```js
const {net} = require('electron').remote
const request = net.request('https://www.baidu.com')
request.on('response', (response)=>{
  console.log(`status: ${response.statusCode}`)
  console.log(`header: ${JSON.stringify(response.headers)}`)
  response.on('data', (chunk)=>{
    console.log("接收到的数据", chunk.toString())
  })
  response.on('end', ()=>{console.log("接收数据完成")})
})
request.end()
```

## 集成vue

### 安装 vue-cli
```shell
npm install -g vue-cli
```
### 创建工程
```shell
vue init simulatedgreg/electron-vue electron-vue-start
```

### 进程工程安装依赖
```shell
cd electron-vue-start
yarn
```
### 启动开发模式
```shell
yarn dev
```



## 应用打包-vue

```shell
yarn build
```

