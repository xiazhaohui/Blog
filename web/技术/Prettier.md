<!--
 * @Author: 夏朝辉 lesslessmore@163.com
 * @Date: 2023-05-30 15:37:14
 * @LastEditors: 夏朝辉 lesslessmore@163.com
 * @LastEditTime: 2023-05-30 15:40:50
-->
# Prettier

**prettier**是一个格式化工具，根据具体语法进行格式化，使项目代码风格趋于统一化

**安装**

```bash
npm install prettier -D
```

**使用**

在根目录新建文件`.prettierrc`，并写入相关配置

```tsx
{
 // 对象的最后一个属性末尾也会添加逗号：","
  "trailingComma": "all",
 // 缩进大小
  "tabWidth": 2,
 // 是否添加分号
 "semi": false,
 // 是否单引号 
  "singleQuote": true,
 // jsx语法下是否单引号
  "jsxSingleQuote": true,
  "endOfLine": "lf",
 // 单行代码最长字符长度
  "printWidth": 120,
  "proseWrap": "never",
 // 在对象中的括号中打空格
  "bracketSpacing": true,
 // 箭头函数的参数无论有几个，都添加括号
  "arrowParens": "always",
  "overrides": [
    {
      "files": ".prettierrc",
      "options": {
        "parser": "json"
      }
    }
  ]
}
```

**配置自动保存时格式化代码**

在根目录下新建文件夹`.vscode`，在文件夹中新建文件`settings.json`

```json
{
 // 指定那些文件不参与搜索
  "search.exclude": {
    "**/node_modules": true,
    "dist": true,
    "build": true
  },
 // 保存时，自动执行一次代码格式化
  "editor.formatOnSave": true,
  "[css]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[scss]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[javascript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[javascriptreact]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[typescript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[typescriptreact]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[json]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  }
}
```

在根目录下创建`.prettierignore`文件，配置后，可忽略某些文件的格式化和自动修复

```json
/node_modules
/build
/dist
```

**注意事项：**
其配置可能会与别的配置有冲突，例如EditorConfig，所以在进行配置时，最好是设置相同的值。

**参考文档：**

[https://www.prettier.cn/docs/index.html](https://www.prettier.cn/docs/index.html)
