# vscode 的任务体系及配置
在日常的开发中我们通常会将一些常用操作（例如编译）封装到特定的命令中，比如经典的工具 `make` 。但这样的策略会使得只能通过在控制台中执行特定语句的方式去执行这些操作，难以配合 `vscode` 的 `debug` 功能。

比如我需要启动在 `launch.json` 中配置的调试服务前执行一个编译任务的话，只能先手动执行该编译任务，然后通过 `vscode` 的 `debug` 功能启动 `launch.json` 中的服务。 

通过将常用操作的封装到 `vscode` 的 `tasks.json` 的方式，我们可以在 `launch.json` 中引用这些 `task` ，实现在启动某个调试服务前自动执行特定的任务，减少手动操作的步骤。

## 创建任务
在 `.vscode` 目录下创建 `tasks.json` ，然后即可在 `tasks` 这一项中添加自定义的任务任务。
```json
// tasks.json
{
    "version": "2.0.0",
    "tasks": [...]
}
```

需要注意的这里的 `version` 表示 `vscode` 中对 `tasks.json` 解析的策略，目前有两个版本 `0.1.0` 与 `2.0.0`，这里以 `2.0.0` 为标准。

## 任务配置
```json
// tasks.json
{
    "version": "2.0.0",
    "tasks": [
        {
            "label": "first try",
            "type": "shell",
            "command": "ls",
            "windows": {
                "command": "dir"
            }
        }
    ]
}
```
这里定义了一个名为 `first try` 的任务，任务执行的是输出当前目录下的文件信息。

## 单独调出任务
点击菜单栏中的 `任务` 选择 `运行任务` 即可在弹出的下拉框中选择想要执行的任务。不过单独调出不是很常用，也不是这块常用的地方（不如绑定快捷键与直接执行命令方便）

## 与 `launch.json` 中调试的配合
在 `launch.json` 中相应的 `launch` 中添加 `"preLaunchTask": <任务的名称>` 即可在相应的 `debug` 启动前执行特定的任务。

需要注意的是这里的 `preLaunchTask` 所对应的任务的 `isBackground` 属性需要为 `false`，否则 `launch` 无法判断任务是否执行完毕。

// TODO `isBackground` 部分需要额外试验

## 详细参考
[vscode tasks使用官方文档](https://code.visualstudio.com/docs/editor/tasks)
