<!--
 * @Author: 夏朝辉 lesslessmore@163.com
 * @Date: 2023-05-30 15:46:00
 * @LastEditors: 夏朝辉 lesslessmore@163.com
 * @LastEditTime: 2023-05-30 15:46:01
-->
# Monorepo

monorepo(monolithic repository)是管理项目代码的一个方式，把多个项目的所有代码放到一个 git仓库中进行管理。

优点：

- 工作流一致
- 项目基建成本低
- 团队协作更容易

基于 Monorepo 的项目管理，不是仅仅代码放到一起就可以的，还需要考虑项目间依赖分析、依赖安装、构建流程、测试流程、CI 及发布流程等诸多工程环节，同时还要考虑项目规模到达一定程度后的性能问题，比如项目构建/测试时间过长需要进行增量构建/测试、按需执行 CI等等。

# 使用`pnpm` + `monorepo`构建多包管理项目

**初始化**

```bash
pnpm init
```

**创建`pnpm-workspace.yaml`文件**

这个文件定义了工作空间的根目录

```yaml
packages:
  - 'packages/ **'
```

创建一个放置多包项目的文件夹，在内部创建项目，给项目的package.json文件修改名字，方便后面引用

```
monorepo-demo
├── package.json
├── packages
│   ├── project-one
│   │   ├── index.js
│   │   └── package.json
│   ├── project-two
│   │   ├── index.js
│   │   └── package.json
├── pnpm-lock.yaml
└── pnpm-workspace.yaml
```

project-one子项目

```json
{
  "name": "@packages/project-one",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "type": "module",
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "moment": "^2.29.4"
  }
}
```

project-two子项目

```json
{
  "name": "@packages/project-two",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "type": "module",
  "keywords": [],
  "author": "",
  "license": "ISC"
}
```

安装依赖

在某个项目中安装依赖，可以使用pnpm的`--filter`命令，其缩写方式为`-F`

```bash
pnpm -F @packages/project-one add moment
```

在project-one项目中引用project-two的包，@\\*表示默认同步最新版本

> 如果不能运行，则在*号前面加斜杠，转义一下
>

```bash
pnpm -F @packages/project-one add @packages/project-two@\*
```

**运行**

```bash
node packages/project-one
```
