## Electron 渲染进程调用主进程函数/主进程与渲染进程之间的通信

在 Electron 中，渲染进程不能直接调用主进程的函数，但可以通过**IPC通信机制**实现这一目的。

### 渲染进程向主进程发送消息

渲染进程可以使用 `ipcRenderer` 发送消息到主进程，主进程使用 `ipcMain` 接收并处理这些消息。反之亦然。

#### 示例

- **主进程**：
  
  ```javascript
  const { ipcMain } = require('electron');
  ipcMain.handle('some-channel', async (event, args) => {
    // 处理渲染进程的请求
    return 'response from main process';
  });

- **渲染进程**

  ```javascript
  const { ipcRenderer } = require('electron');
  async function callMainProcess() {
    const response = await ipcRenderer.invoke('some-channel', 'some-args');
    console.log(response); // 输出 'response from main process'
  }
  callMainProcess();
  ```

### 主进程向渲染进程发送消息

在 Electron 中，主进程可以通过 `webContents.send` 方法向渲染进程发送消息。

#### 示例

- **主进程**：
  ```javascript
  const { app, BrowserWindow } = require('electron');
  let mainWindow;
  
  app.on('ready', () => {
    mainWindow = new BrowserWindow({
      width: 800,
      height: 600,
      webPreferences: {
        preload: path.join(__dirname, 'preload.js')
      }
    });
  
    mainWindow.loadFile('index.html');
  
    // 在窗口加载完成后发送消息
    mainWindow.webContents.on('did-finish-load', () => {
      mainWindow.webContents.send('message-from-main', 'Hello from Main Process');
    });
  });

- **渲染进程**

  ```javascript
  const { ipcRenderer } = require('electron');
  
  ipcRenderer.on('message-from-main', (event, message) => {
    console.log(message); // 输出 'Hello from Main Process'
  });
  ```

  
