## Electron主进程和渲染进程间的通信

### 异步通信

渲染进程给主进程发送消息：

```javascript
const {ipcRenderer} = require('electron')

//向主进程发送消息
ipcRenderer.send('name', 'nebulau')
```

主进程接收渲染进程消息：

```javascript
ipcMain.on('name', (ev, data)=>{
    console.log(data)
})
```

主进程给渲染进程发送消息：

```javascript
ipcMain.on('name', (ev, data)=>{
    console.log(data)
    ev.sender.send('reply', 'recved name: ' + data)
})
```

渲染进程接收主进程消息：

```javascript
const {ipcRenderer} = require('electron')

//向主进程发送消息
ipcRenderer.on('reply', (ev, data)=>{
	console.log(data)
})
```

###  同步通信

渲染进程给主进程发送消息：

```javascript
const {ipcRenderer} = require('electron')

//向主进程发送消息
ipcRenderer.sendSync('name', 'nebulau')
```

主进程接收渲染进程消息代码和异步通信代码相同

