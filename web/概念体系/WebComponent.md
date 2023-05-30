<!--
 * @Author: 夏朝辉 lesslessmore@163.com
 * @Date: 2023-05-30 14:18:17
 * @LastEditors: 夏朝辉 lesslessmore@163.com
 * @LastEditTime: 2023-05-30 14:23:37
-->
# WebComponent

组件化的原则：对内**高内聚**，对外**低耦合**

WebComponent 是一套技术的组合，具体涉及到了 Custom elements（自定义元素）、Shadow DOM（影子 DOM）和HTML templates（HTML 模板）。WebComponent提供了对局部视图封装能力，可以让DOM、CSSOM和JavaScript运行在局部环境中，这样就使得局部的CSS和DOM不会影响到全局。

shadowDOM

shadowDOM的作用是将模板中的内容与全局 DOM 和 CSS 进行隔离，这样就可以实现元素和样式的私有化（shadowDOM的JavaScript 脚本不会被隔离）

内部的样式和元素不会影响到全局的样式和元素，在全局环境下，要访问影子 DOM 内部的样式或者元素需要通过约定好的接口来实现
