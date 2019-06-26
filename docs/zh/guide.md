---
editLink: https://github.com/WittBulter/func/blob/master/docs/zh/guide.md
---

# 快速上手
## 创建项目
`func` 提供了安装脚本与默认的项目模板，如果你想创建一个项目，只需要一个命令就可以完成：

```bash
npm init func
```
::: tip 提示
这需要你的 `npm` 版本 > 6.1.0 。
:::

## 快速开发

进入刚刚初始化项目的项目后，你可以见到以下的项目结构:

```
|--src
    |--commands         // 命令
    |--options          // Option 风格命令
    |--index.ts         // 入口
|--tests            // 测试用例
|--package.json
```

你可以运行以下命令以开始开发:
```bash
npm i && npm start      # 更新依赖并准备开发环境
```

至此为止，所有的准备事项都已完毕，你可以浏览 `commands` / `options` 中的示例，尝试修改它们并运行您的命令，看看效果如何。

有人可能会疑惑，那我的命令是什么。其实就是你文件夹的名字，你可以注意到 `package.json` 中有 `bin` 这一项，这用于定义你的命令，
默认是你的项目名 (在初始化模板时指定的)。当然，你可以随时修改它，只要别忘了在修改后运行一次 `npm start` 初始化就可以了。

## 打包

如果你是使用模板创建的项目，只需要执行一个命令即可将项目打包：
```bash
npm build
```

很简单是吧？运行 `npm build` 你可以得到一个打包后的文件，同时也为你处理好了 `bin`，什么都不用考虑，试试直接发布它吧。

:::warning
运行 build 后项目会指向生产，如果需要返回开发模式，还是运行 `npm start` 即可。
:::

## 发布

你可以参照 [如何发布的文档](/zh//publish.md) 学习更多的发布技巧，但现在我们不必在乎太多，试试用 `npm publish` 在 NPM 上直接发布你的包吧！

然后试试安装自己的包，怎么样，是不是很快，一切都这么简单，这就是 `func` 的魅力。