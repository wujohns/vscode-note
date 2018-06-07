# vscode 中的配置同步
工作后一般会出现家里一台电脑，公司一台电脑的场景，为了保持不同设备上的 ide 配置一致，可以使用 ide 的配置同步功能，`vscode` 提供了基于 `github` 的同步策略。

## 依赖
需要安装插件 [Settings Sync](https://marketplace.visualstudio.com/items?itemName=Shan.code-settings-sync)

在 `github` 中创建用于同步的 `token`，[页面](https://github.com/settings/tokens)，在创建时勾选 `gist Create gists` 选项。

## 配置
完成上述依赖的工作后，在 `vscode` 中 `alt+shift+u`，将上述创建的 `token` 复制到弹出框中然后 `Enter`，即可将正在使用的 `vscode` 中的配置上传到 `github` 中。

在另外一台设备上的 `vscode` 中 `alt+shift+d`，将上述创建的 `token` 复制到弹出框中然后 `Enter`，即可下载相应的配置。

配置可以在 [gist 页面](https://gist.github.com/) 的 `codeSettings`。

## 使用
在配置完成后，每次修改了 `vscode` 的配置需要上传时则执行 `alt+shift+u`，需要下载存储在 `github` 上的 `vscode` 配置时执行 `alt+shift+d` 即可：

```
alt+shift+u -- upload
alt+shift+d -- download
```

## 进阶配置
### 重置
使用 `ctrl+shift+p` 打开命令栏后，找到 `Sync: Reset Extension Settings` 即可重置

### 配置自动上传与自动下载
使用 `ctrl+shift+p` 打开命令栏后，找到 `Sync: Advanced Options`，点击进入后选择 `Toggle Auto-Upload on Settings Change` 即可开关 `自动保存上传功能`  
使用 `ctrl+shift+p` 打开命令栏后，找到 `Sync: Advanced Options`，点击进入后选择 `Toggle Auto-Download On Startup` 即可开关 `启动时自动下载功能`

上述配置后，会在 `vscode` 右下角弹出提示，表明进入到那种状态