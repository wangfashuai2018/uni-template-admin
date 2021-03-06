# uni-template-admin

> 基于 uni-app，uniCloud 的 admin 管理项目模板

---

-   [使用](#使用)
    -   [创建](#创建)
    -   [运行](#运行)
-   [目录结构](#目录结构)
-   [顶部窗口（导航栏）](#顶部窗口导航栏)
-   [左侧窗口（菜单栏）](#左侧窗口菜单栏)
-   [用户系统](#用户系统)
-   [权限系统](#权限系统)
-   [插件](#插件)
    -   [开发 admin 插件](#开发-admin-插件)
    -   [使用 admin 插件](#使用-admin-插件)
    -   [admin 插件列表](#admin-插件列表)

### 使用

#### 创建

方式一：[HBuilderX](https://www.dcloud.io/hbuilderx.html) 新建 uni-app 项目，选择 uniCloud admin 项目模板。

方式二：[插件市场](https://ext.dcloud.net.cn/)，使用 HBuilderX 导入。

方式三：[下载压缩包](https://github.com/dcloudio/uni-template-admin/archive/master.zip)，解压后，导入 HBuilderX。

#### 运行

1. 进入 admin 项目
2. 右键 cloudfuntions 绑定服务空间
3. 右键 cloudfuntions 上传所有云函数及公共模块
4. 右键 db_init.json 初始化云数据库
5. 点击工具栏的运行 -> 运行到浏览器

### 目录结构

```bash
├── cloudfunctions              # 云函数
├── components                  # 自定义组件
├── js_sdk                      # js sdk
├── pages                       # 页面
│   │── index                   # 首页
│   └── login                   # 登录页
├── static
├── store                       # vuex
├── windows
│   └── leftWindow.vue          # 左侧窗口（菜单栏）
│   └── topWindow.vue           # 顶部窗口（导航栏）
├── admin.config.js             # 系统配置（配置导航，菜单等）
├── App.vue
├── main.js
├── mainfest.json
├── pages.json
├── postcss.config.js           # postcss 配置（浏览器兼容性）
└── uni.scss
```

### 顶部窗口（导航栏）

> 源码 [windows/topWindow.vue](https://github.com/dcloudio/uni-template-admin/blob/master/windows/topWindow.vue)

1. 通过 [admin.config.js](https://github.com/dcloudio/uni-template-admin/blob/master/admin.config.js) 配置导航栏内容

```js
export default {
    // 导航栏
    navBar: {
        // 左侧 Logo
        logo: "/static/logo.png",
        // 右侧链接
        links: [
            {
                text: "项目文档",
                url:
                    "https://github.com/dcloudio/uni-template-admin/blob/master/README.md",
            },
        ],
    },
};
```

2. 通过 [uni.scss](https://github.com/dcloudio/uni-template-admin/blob/master/uni.scss) 配置导航栏样式

```css
$top-window-bg-color: #fff; /* 背景色 */
$top-window-text-color: #999; /* 文字颜色 */
```

### 左侧窗口（菜单栏）

> 源码 [windows/leftWindow.vue](https://github.com/dcloudio/uni-template-admin/blob/master/windows/leftWindow.vue)

1. 通过 [admin.config.js](https://github.com/dcloudio/uni-template-admin/blob/master/admin.config.js) 配置侧边栏内容

```js
export default {
    // 侧边栏
    sideBar: {
        // 配置静态菜单列表（放置在用户被授权的菜单列表下边）
        secondaryMenus: [
            {
                name: "404页面",
                url: "/pages/error/404",
            },
        ],
    },
};
```

2. 通过 [uni.scss](https://github.com/dcloudio/uni-template-admin/blob/master/uni.scss) 配置侧边栏样式

```css
$left-window-bg-color: #fff; /* 侧边栏背景色 */
$menu-bg-color: #fff; /* 一级菜单背景色 */
$sub-menu-bg-color: darken($menu-bg-color, 10%); /* 二级以下菜单背景色 */
$menu-bg-color-hover: darken($menu-bg-color, 13%); /* 菜单 hover 背景颜色 */
$menu-text-color: #333; /* 菜单前景色 */
$menu-text-color-actived: #007aff; /* 菜单激活前景色 */
```

### 新增页面

1. 新增前端 vue 页面

2. 新增后端 api 接口

### 用户系统

> 基于 [uni-id](https://uniapp.dcloud.io/uniCloud/uni-id) 用户登录

1.  用户登录

-   源码 [pages/login/login.vue](https://github.com/dcloudio/uni-template-admin/blob/master/pages/login/login.vue)
-   通过 [admin.config.js](https://github.com/dcloudio/uni-template-admin/blob/master/admin.config.js) 自定义登录页面路径

```js
export default {
    login: {
        url: "/pages/login/login", // 登录页面路径
    },
};
```

### 权限系统

> 基于 [uni-id](https://uniapp.dcloud.io/uniCloud/uni-id?id=rbac-api) 角色权限

1. 用户管理
    > [详情](https://github.com/dcloudio/uni-template-admin/tree/master/uni_modules/admin-user)
2. 角色管理
    > [详情](https://github.com/dcloudio/uni-template-admin/tree/master/uni_modules/admin-role)
3. 权限管理
    > [详情](https://github.com/dcloudio/uni-template-admin/tree/master/uni_modules/admin-permission)
4. 菜单管理
    > [详情](https://github.com/dcloudio/uni-template-admin/tree/master/uni_modules/admin-menu)
5. 权限验证
    ```html
    <template>
        <view>
            <!-- 包含 user/add 权限的用户可以看到新增按钮 -->
            <button v-if="$hasPermission('user/add')">新增</button>
            <!-- 包含 admin 角色的用户可以看到删除按钮 -->
            <button v-if="$hasRole('admin')">删除</button>
        </view>
    </template>
    ```

### 插件

#### 开发 admin 插件

> TODO

#### 使用 admin 插件

> TODO

#### admin 插件列表

-   [菜单管理](https://github.com/dcloudio/uni-template-admin/tree/master/uni_modules/admin-menu)
-   [权限管理](https://github.com/dcloudio/uni-template-admin/tree/master/uni_modules/admin-permission)
-   [角色管理](https://github.com/dcloudio/uni-template-admin/tree/master/uni_modules/admin-role)
-   [用户管理](https://github.com/dcloudio/uni-template-admin/tree/master/uni_modules/admin-user)
-   [云存储管理](https://github.com/dcloudio/uni-template-admin/tree/master/uni_modules/admin-storage)

### 进阶

##### 如何使用 element-ui

1. 根目录，命令行执行：`npm i element-ui -S`
2. 根目录，修改 `template.h5.html`，引用 `element-ui` 的 `index.css` 文件

    注：在 html 中直接引入后，请不要在 js 中再引入该 css 文件

```html
<!-- 若使用了 element-ui 组件，可取消下一行的 css 引用注释，注意：不要在 js 中重复引入该 css -->
<link
    rel="stylesheet"
    href="<%= BASE_URL %>static/element-ui/lib/theme-chalk/index.css"
/>
```

3. `pages.json` 中已内置 `element-ui` 的 `easycom` 配置，可以直接在 `template` 中使用 `el-` 开头的组件

```html
<template>
    <view>
        <el-tag>标签一</el-tag>
        <el-tag type="success">标签二</el-tag>
        <el-tag type="info">标签三</el-tag>
        <el-tag type="warning">标签四</el-tag>
        <el-tag type="danger">标签五</el-tag>
    </view>
</template>
```
