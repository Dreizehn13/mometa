<p align="center">
  <img src="./images/logo.png" />
</p>
<p align="center">
  <a href="https://travis-ci.org/imcuttle/mometa"><img src="https://img.shields.io/travis/imcuttle/mometa/master.svg?style=flat-square" /></a>
  <a href="https://codecov.io/github/imcuttle/mometa?branch=master"><img src="https://img.shields.io/codecov/c/github/imcuttle/mometa.svg?style=flat-square" /></a>
  <a href="https://prettier.io/"><img src="https://img.shields.io/badge/code_style-prettier-ff69b4.svg?style=flat-square" /></a>
  <a href="https://lernajs.io/"><img src="https://img.shields.io/badge/maintained%20with-lerna-cc00ff.svg?style=flat-square" /></a>
  <a href="https://conventionalcommits.org"><img src="https://img.shields.io/badge/Conventional%20Commits-1.0.0-yellow.svg?style=flat-square" /></a>
</p>
<p align="center">面向研发的低代码元编程（代码可视化）能力</p>

<p align="center">
  <img src="./images/snapshot.png" />
</p>

## 特性

- 面向研发的代码可视化编辑
- 开放物料生态，可定制团队内物料库，见 [mometa-mat](https://github.com/imcuttle/mometa-mat)
- 多语言、多生态支持，目前暂只支持 React
- 接入友好，Webpack 0 成本接入
- 开发友好，物料库支持热更新，不破坏已有开发模式

## 为什么需要 Mometa

1.  新同学上手物料库，传统方式学习成本高，不能所见即所得编辑
2.  对于一些重复场景的代码模板，业务组件，不能快速的查阅和引入
3.  团队打造属于自己业务场景下的 代码模板，业务组件

## 操作演示

#### 预览

<p align="center">
  <img src="./images/mometa-preview.gif" />
</p>

#### 编辑

<p align="center">
  <img src="./images/mometa-edit.gif" />
</p>

## 如何使用

#### 安装依赖

```bash
npm i @mometa/materials-generator @mometa/editor -D
```

#### 使用 antd 物料

1.  安装 antd 物料

```bash
npm i @mometa-mat/antd -D
```

2.  在项目根目录中创建 `mometa-material.config.js`

```jsx
const { resolveLibMatConfig } = require('@mometa/materials-generator')

module.exports = [resolveLibMatConfig('antd')]
```

你也可以创建自己的物料库，数据结构规则见 [Material 定义](./packages/materials-generator/src/types.ts)

#### 接入编辑器

`webpack.config.js` 修改如下：

```js
const MometaEditorPlugin = require('@mometa/editor/webpack')

module.exports = {
  module: {
    rules: [
      {
        test: /\.(js|mjs|jsx|ts|tsx)$/,
        // 注意，只需要处理你需要编辑的文件目录
        include: paths.appSrc,
        loader: require.resolve('babel-loader'),
        options: {
          plugins: [isEnvDevelopment && require.resolve('@mometa/editor/babel/plugin-react-runtime')]
        }
      }
    ]
  },
  plugins: [isEnvDevelopment && new MometaEditorPlugin()]
}
```

**注意：使用时，不需要开启官方预设的 react-refresh，mometa 默认会开启 react-refresh 能力**

提供的例子可见 [@mometa/app](./packages/app)

## Packages

- [@mometa/editor](packages/editor) - 编辑器
- [@mometa/fs-handler](packages/fs-handler) - 代码操作转换核心逻辑，如删除、移动、替换、插入等
- [@mometa/materials-generator](packages/materials-generator) - 物料生成器
- [@mometa/react-refresh-webpack-plugin](packages/react-refresh-webpack-plugin) - An **EXPERIMENTAL** Webpack plugin to enable "Fast Refresh" (also previously known as _Hot Reloading_) for React components.

## Contributing

- Fork it!
- Create your new branch:\
  `git checkout -b feature-new` or `git checkout -b fix-which-bug`
- Start your magic work now
- Make sure npm test passes
- Commit your changes:\
  `git commit -am 'feat: some description (close #123)'` or `git commit -am 'fix: some description (fix #123)'`
- Push to the branch: `git push`
- Submit a pull request :)

## Authors

This library is written and maintained by imcuttle, <a href="mailto:imcuttle@163.com">imcuttle@163.com</a>.

## License

MIT - [imcuttle](https://github.com/imcuttle) 🐟
