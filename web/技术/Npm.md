<!--
 * @Author: 夏朝辉 lesslessmore@163.com
 * @Date: 2023-05-30 15:36:55
 * @LastEditors: 夏朝辉 lesslessmore@163.com
 * @LastEditTime: 2023-05-30 15:39:49
-->
# Npm

版本号语义化理解

> major.minor.patch[-prerelease]
>
> 主版本号-次版本号-修复版本号[-测试版本号/标签]

版本号结构

通常由四部分组成，例如（1.2.3-beta.1）

- `maior`表示主版本号，新增功能，不向下兼容
- `minor`表示次版本号，新增功能，向下兼容
- `patch`表示修复/补丁版本号，修复某些BUG
- `prerelease`表示测试版本号，不稳定
  - alpha：内测版标签，很多BUG
  - beta：尚有BUG版标签
  - rc：正式版前的最后一个候选测试版标签

dist-tag标签：

默认情况下，`npm publish`时使用`latest`标记，若要使用其他标签，可通过`—-tag`标记

发布带标签的版本：`npm publish —tag <标签>`

把标签标记到指定包版本：`npm dist-tag add <包名>@<版本号> [<标签>]`

示例；

```tsx
npm publish --tag beta

npm dist-tag add 包名@3.0.0 beta
```

在版本迭代时，标签只能指向一个版本号，且：

latest标签永远指向最新的稳定版本；

beta标签永远指向最新的公测版本

安装命令

| 命令 | 说明 |
| --- | --- |
| npm install react
npm install react@lastly | 安装最新版 |
| npm install react@17.0.1 | 安装指定版本 |
| npm dist-tag ls | 查看标签 |

版本升级工具`npm version`：自动修改package.json中的版本号，并且自动git commit

升级主版本号：`npm version major`

升级次版本号：`npm version minor`

升级补丁修复版本号：`npm version patch`

升级测试版本号： `npm version prerelease`

发布包：`npm publish`

---

**流程**：

1. 新建一个空文件夹
2. 生成package.json配置信息
3. 写包要实现的功能
4. 登陆npm
5. 发布

package.json文件

必填项：name、version

```json
{
  "name": "npm-silly",
  "version": "4.0.0",
  "description": "first npm demo",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "silly",
  "license": "ISC"
}
```

文件目录管理：

所有包都需要一个 **index.js**文件。这是包的入口文件

![Untitled](/assets/web/技术/npm-1.png)

模拟操作：

- 新建包

```bash
mkdir npm-demo
cd npm-demo
touch indedx.js

npm init 
npm login
```

- git管理

```bash
git init
git remote add origin xxx
```

- 发布包

```bash
npm publish
```

- 升级主版本

```bash
npm version major
```

- 升级次版本

```bash
npm version minor
```

- 升级补丁修复版

```bash
npm version patch
```

- 升级测试版本号

```bash
npm version prerelease
```

- 升级版本号时打标签

```bash
npm publish --tag beta
```

- 给特定版本号打标签

```bash
npm dist-tag add 包名@3.0.0 beta
```

- 查看当前包的版本和标签

```bash
npm dist-tag ls
```

- 取消/撤销某版本号

[npm-silly](https://www.npmjs.com/package/npm-silly)
