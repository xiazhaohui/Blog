<!--
 * @Author: 夏朝辉 lesslessmore@163.com
 * @Date: 2023-05-30 15:37:02
 * @LastEditors: 夏朝辉 lesslessmore@163.com
 * @LastEditTime: 2023-05-30 15:40:32
-->
# pnpm

新一代包管理工具

幽灵依赖：没有显式依赖（声明在dependencies里面的依赖），但是却可以在代码里面引用，不知何时就无法正常使用

> npm2 是通过嵌套的方式管理 node_modules 的，会有同样的依赖复制多次的问题
>
> npm3+ 和 yarn 是通过铺平的扁平化的方式来管理 node_modules，解决了嵌套方式的部分问题，但是引入了幽灵依赖的问题，并且同名的包只会提升一个版本的，其余的版本依然会复制多次。
> pnpm通过软链接来组织依赖关系

pnpm

一个包全局只保存一份，包和包之前的依赖关系是通过软链接组织的。

包是从全局 store 硬连接到虚拟 store 的， node_modules/.pnpm就是虚拟store，

优点：

- 节省磁盘空间
- 安装速度快
- 解决幽灵依赖
