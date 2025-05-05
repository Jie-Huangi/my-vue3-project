# 备忘录应用

## 简介

这是一个简单的备忘录应用，使用 Vue 3 和 uni-app 框架开发。

## 功能

- 用户可以注册和登录
- 登录后，用户可以创建、编辑和删除备忘录
- 应用提供首页和备忘录页面，方便用户切换

## 技术栈

- Vue 3
- uni-app
- SCSS

## 目录结构

```
├── .gitignore
├── index.html
├── login-prototype.html
├── package-lock.json
├── package.json
├── README.md
├── shims-uni.d.ts
├── src
│   ├── App.vue
│   ├── main.js
│   ├── manifest.json
│   ├── pages.json
│   ├── pages
│   │   ├── index
│   │   │   └── index.vue
│   │   ├── login
│   │   │   └── index.vue
│   │   ├── memo
│   │   │   ├── add.vue
│   │   │   ├── detail.vue
│   │   │   └── index.vue
│   │   └── register
│   │       └── index.vue
│   ├── static
│   │   ├── iconfont.css
│   │   └── logo.png
│   ├── uni.scss
│   └── vite.config.js
└── vite.config.js
```

## 运行

1. 安装依赖

```bash
npm install
```

2. 运行应用

```bash
npm run dev:h5
```

## 注意

- 本应用仅为示例，数据存储在本地，没有后端支持。

## License

MIT
