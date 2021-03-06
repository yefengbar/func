# 命令

## 创建 Command 命令

在 `func` 中，创建命令非常的简单，你只需要为任何一个类添加 `Command` 注解即可：

```ts
@Command({
  name: 'hello',
})
export class MyFirstCommand {
  constructor() { console.log('ok') }
}
```

假设你的命令行工具的名称是 "hello-func"，现在只需要运行 `hello-func hello` 终端就会显示 `ok`。一切就这么成了。

<img src="/../hello-func-3.png" width="350">

这个 `MyFirstCommand` 类和你通常写的类没有什么不同，它只是在运行命令时会被自动的调用而已，一切都是那么熟悉，你可以在类中写任何你喜欢的逻辑。

## 创建 Option 命令

我们知道，命令行工具通常还会有一些顶级的选项，就拿你的 "tools" 来说，你也许会希望它有 `<command> --version` 等功能作为支持。

这里，我们可以使用 `Option` 装饰器非常优雅实现：

```ts
import { Option } from 'func'

@Option({
  name: 'version',
  alias: 'v',
})
export class Version {
  constructor() { console.log('1.0.0') }
}
```

为你的类 `Version` 添加了一些信息后，它会在 `--version` 和 `-v` 时被触发。

<img src="/../hello-func-4.png" width="350">

这很简单，`-v` 是它的别名。

`func` 允许你为任何命令创建别名，如果是 `Option` 命令的别名，只需要一个 `-` 就可以调用，这也很标准。

## 子选项

在 func 的内部，也为你准备好了一个装饰器 `SubOptions` 实现类似于 `<command> --<option>` 这样的命令:

```ts
@Command({
  name: 'apple',
})
@SubOptions([{ name: 'help', alias: 'h' }])
export class MyFirstSubOption {

  constructor(
    private arg: CommandArgsProvider,
  ) {
    if (arg.option.help) {
      console.log('HELP MESSAGE: The apple is red')
    }
    console.log('ok')
  }
  
}
```

<br/>
<img src="/../hello-func-5.png" width="380">

这样就可以使用在命令 `test` 的基础上为其增加 `--help` 的选项。

有关于如何获取选项的值，请参见 [参数获取](/zh/params.md) 章节。

## 主命令

主命令指的是仅仅运行你命令行的名字，没有携带任何参数的场景:

```ts
import { CommandMajor } from 'func'

@CommandMajor()
export class Main {
}
```

如果你的命令行工具还是叫做 `tools`，那么只运行 `tools` 就会触发主命令了。

## 无法找到的命令

少数时候，用户可能会错误的输入参数或命令，你需要友好的提示一些信息并指引用户，`CommandMissing` 就是用来解决这个问题的。
在没有任何 `Command` 或 `Option` 被找到时就会触发无法找到：

```ts
import { CommandMissing } from 'func'

@CommandMissing()
export class Missing {
  constructor() { console.log('not found any commands!') }
}
```


