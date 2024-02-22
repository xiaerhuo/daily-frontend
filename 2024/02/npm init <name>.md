# npm init `<packageName>`

在 `npm@6.1.0` 里增加了 `npm init <packageName>` 这种操作，当执行 `npm init <packageName>` 时，`packageName` 是一个名为 `create-<packageName>` 的 `npm` 包，它将由 `npm-exec` 安装，然后执行其主 `bin` —— 大概是创建或更新 `package.json` 并运行任何其他与初始化相关的操作。

`init` 命令转化为对应的 `npm exec` 操作如下：

```shell
npm init foo -> npm exec create-foo
npm init @usr/foo -> npm exec @usr/create-foo
npm init @usr -> npm exec @usr/create
```

执行 `npm exec create-<packageName>` 时，主要经历下面两个步骤：

1. `npm` 将 `create-<packageName>` 仓库下载到一个临时目录，使用以后会删除掉，这样就减少了 `create-<packageName>` 的全局安装
2. 执行主bin `create-<packageName>` 命令，最终完成脚手架的启动

## 参考文档

1. [npm init官方文档](https://www.npmjs.cn/cli/init/)
