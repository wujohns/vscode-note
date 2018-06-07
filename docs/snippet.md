# vscode sinppet 的使用
在日常的工作中，经常会有重复用到的代码片段，但相应的代码片段又不足以达到单独写一个包的地步，这时就可以考虑使用 `vscode` 的 `sinppet` （代码片段）特性，将代码片段添加到于 `vscode` 中，在编写代码时以智能提示的方式快捷的使用添加的代码片段，加快开发速度。

## 进入 sinppet 配置
1. 点击 `vscode` 右下角齿轮图标，在弹出的菜单中选择 `用户代码片段`  
1. 选择自己需要配置的语言，会打开指定语言的 `sinppet` 配置文件（json格式）  
1. 如果需要做更细致的分类，也可以选择创建新的 `sinnpet`

备注：在进入到代码片段管理时，会有一个 `现有代码片段` 的列表，创建的代码片段配置（json文件）会被存储到指定的地方，若想删除则可以切换到相应的目录删除即可。

如果是选取指定的语言创建 `sinppet` ，那么 `vscode` 中对应的配置文件名称为 `<语言名称>.json`  
如果是选取 `新建全局代码片段文件`，那么则需要在相应配置文件中则需要配置 `scope` 参数指定是适配那种语言。

## sinppet 配置规则
### 添加单个片段的案例
```json
{
    "ccc test sinnpet": {
        "scope": "javascript",  // 该 sinnpet 适配 javascript
        "prefix": "cct",        // sinnpet 的关键字（在js文件中输入 "cct" 时就会出现该 sinnept 的提示 ）
        "body": [       // 模板的主体内容，数组中的每一项代表一行
            "console.log(`test $1`);",
            "$2"
        ],
        "description": "测试"   // 呼出该 sinnpet 时的文字提示
    }
}
```

将上述代码片段添加到 `vscode` 后，再在 `vscode` 中编辑 js 文件时，输入 `cct` 即能呼出该代码片段，选中后即可自动在编辑器中输入：  

```js
console.log(`test `);

```

且光标位于 $1 处（使用方向键向下可移动光标到 $2 处）

## body 字段说明
### 基础使用
```json
// 包含默认值的设定
"ex2": {
    "scope": "javascript",
    "prefix": "cc2",
    "body": [
        "console.log(`test ${1:foo}`);",    // 代码生成后这里光标的默认值为 foo
        "$2"
    ],
    "description": "ccc默认值测试"   // 呼出该 sinnpet 时的文字提示
},

// 可选默认值
"ex3": {
    "scope": "javascript",
    "prefix": "cc3",
    "body": [
        "console.log(`test ${1|foo,bar|}`)",   // 代码生成后这里光标会有可选默认值 foo 与 bar
        "$2"
    ],
    "description": "ccc可选默认值测试"  // 呼出该 sinnpet 时的文字提示
},

// 使用内置变量
"ex4": {
    "scope": "javascript",
    "prefix": "cc4",
    "body": [
        "console.log(`test $TM_DIRECTORY`)",    // 代码生成后这里的值为当前文件所在目录
        "$1"
    ],
    "description": "ccc使用内置变量"    // 呼出该 sinnpet 时的文字提示
}
```

基础的使用部分包含默认值、可选默认值以及内置变量使用，这些使用都很简单，直接参考上述案例即可。

### 进阶使用
变量替换部分，可将指定的变量格式化处理后插入指定位置，目前用不上这样的功能，之后用上后再做记录

一些用到的部分记录：    
| 场景 | 做法 |  
| --- | --- |   
| 将文件名由匈牙利写法转换为驼峰写法(用于类名的生成) | `${TM_FILENAME_BASE/(_|^)([a-zA-Z0-9]+)/${2:/capitalize}/gi}` |  

## 修改自定义代码片段的优先级
默认情况下，自定义代码片段的优先级较低，在用户设置中可以修改（`ctrl+shift+p` 输入 `settings` 找到 `用户配置`），修改其中的 `editor.snippetSuggestions` 选项为 `top` 即可让自定义代码片段在提示中显示在最上面。

备注：默认的 `inline` 基本还是挺不错的，感觉不用修改。

## 具体案例参考
[examples/ccc.code-snippets.json](/examples/ccc.code-snippets.json)

## 参考链接
[Add code snippets for CLANG in VS Code](https://blog.csdn.net/maokelong95/article/details/54379046)

备注：该链接中对内置变量有详细说明，`snippet` 的详细语法可以参考官方给出的 EBNF 范式