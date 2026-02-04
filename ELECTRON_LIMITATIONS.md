# Electron 跨平台能力说明

## Electron 支持的平台
- ✅ Windows 桌面应用
- ✅ macOS 应用
- ✅ Linux 应用
- ❌ **不支持 Android**
- ❌ **不支持 iOS**

## 如果你想开发全平台应用，有以下选择：

### 方案一：Electron + 移动端框架组合
- **桌面端**：使用 Electron (Windows/macOS/Linux)
- **移动端**：使用 React Native、Flutter 或 Ionic

### 方案二：纯移动端跨平台方案
- **React Native**：可构建原生 Android/iOS 应用
- **Flutter**：Google 的 UI 工具包，支持 Android/iOS/Web/桌面
- **Ionic**：基于 Web 技术的混合应用

### 方案三：统一 Web App
- 开发 PWA (Progressive Web App)，可在各平台上通过浏览器访问
- 可以添加到主屏幕，提供类似原生应用的体验

## Electron 开发入门示例

```javascript
// main.js - Electron 主进程文件
const { app, BrowserWindow } = require('electron')
const path = require('path')

function createWindow () {
  const mainWindow = new BrowserWindow({
    width: 800,
    height: 600,
    webPreferences: {
      nodeIntegration: true,
      preload: path.join(__dirname, 'preload.js')
    }
  })

  mainWindow.loadFile('index.html')
}

app.whenReady().then(() => {
  createWindow()

  app.on('activate', function () {
    if (BrowserWindow.getAllWindows().length === 0) createWindow()
  })
})

app.on('window-all-closed', function () {
  if (process.platform !== 'darwin') app.quit()
})
```

如果你确实需要同时支持桌面和移动设备，建议采用混合开发策略。