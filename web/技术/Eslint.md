<!--
 * @Author: 夏朝辉 lesslessmore@163.com
 * @Date: 2023-05-30 15:37:24
 * @LastEditors: 夏朝辉 lesslessmore@163.com
 * @LastEditTime: 2023-05-30 15:41:19
-->
# ESLint

`Eslint`主要为了解决代码质量问题，可以检测BUG，还能自动修复一些问题

**安装**

```bash
npm install eslint -D
```

**初始化配置**

```bash
npx eslint --init
```

> npx的作用：
>
> - 会先去本地 `node_modules` 中找 `eslint` 的执行文件，如果找到了，就直接执行
> - 如果没有找到，就去全局找
> - 如果都没有找到，就下载一个临时的 `eslint` ，用完之后就删除这个临时的包，对本机完全无污染

安装及初始化配置之后，根目录会有一个新文件`.eslintrc.js`

安装Vs code插件：`eslint`

在.vscode/settings.json文件中新增配置信息

```json
{
  "eslint.validate": ["javascript", "javascriptreact", "typescript", "typescriptreact"],
 // 代替 vscode 的ts语法智能提示
  "typescript.tsdk": "./node_modules/typescript/lib",
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true,
  },
}
```

在根目录下创建`.eslintignore`文件，配置后，可忽略某些文件的格式化和自动修复

```json
/node_modules
/build
/dist
```

| 忽略项目 | 注释代码 |
| --- | --- |
| 忽略当前行 | // eslint-disable-line |
| 忽略下一行 | // eslint-disable-next-line |
| 嵌套三元表达式 | /*eslint-disable no-nested-ternary*/ |
| useEffect依赖警告 | //eslint-disable-line react-hooks/exhaustive-deps |
| 使用数组index作为key值 | //eslint-disable-next-line react/no-array-index-key |
| 单行忽略 | // @ts-ignore |

**参考文档：**

[https://github.com/vortesnail/blog/issues/14](https://github.com/vortesnail/blog/issues/14)

[https://eslint.bootcss.com/docs/user-guide/configuring](https://eslint.bootcss.com/docs/user-guide/configuring)
