<!--
 * @Author: 夏朝辉 lesslessmore@163.com
 * @Date: 2023-05-30 15:37:38
 * @LastEditors: 夏朝辉 lesslessmore@163.com
 * @LastEditTime: 2023-05-30 15:41:51
-->
# Stylelint

格式化样式代码的风格

**安装**

```bash
npm install stylelint stylelint-config-standard -D
```

**配置**

在项目根目录创建`.stylelintrc.js`文件，输入以下内容：

```jsx
module.exports = {
 // 扩展，使用 stylelint 已经预设好的一些规则。
  extends: ['stylelint-config-standard', 'stylelint-config-prettier'],
 // 具体的规则
  rules: {
    'comment-empty-line-before': null,
    'declaration-empty-line-before': null,
    'function-name-case': 'lower',
    'no-descending-specificity': null,
    'no-invalid-double-slash-comments': null,
    'rule-empty-line-before': 'always',
  },
 // 忽略配置字段
  ignoreFiles: ['node_modules/**/*', 'build/**/*'],
}
```

> `stylelint-config-prettier`会禁用掉所有和prettier有冲突的规则
>

安装Vs code插件：`stylelint`

在`.vscode/settings.json`文件中，增加以下代码：

```json
{
 // 使用 stylelint 自身的校验即可
  "css.validate": false,
  "less.validate": false,
  "scss.validate": false,
  "editor.formatOnSave": true,
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true,
    "source.fixAll.stylelint": true
  },
}
```

参考文章：

[https://stylelint.io/user-guide/get-started/](https://stylelint.io/user-guide/get-started/)
