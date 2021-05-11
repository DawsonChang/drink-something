# drink-something

## 架構
```
此 project 最主要的部分是 App.vue，部分會跨 component 的變數及函式都定義在此。所有 component 都是透過
callback function 來改變主要變數（變數定義在 App.vue），這些 callback function 當作 props 傳入
child component。

其中靜態資料定義在 src/data/orders.json

各個 component 介紹 (src/components):
    Card.vue - 單一 order 的排版和 style
    List.vue - 用 v-for 將所有 order 用 Card component 顯示出來
    Modal.vue - 顯示一個獨立視窗，用來新增、編輯、刪除
    TitleSection.vue - 負責標題、新增按鈕、排列選單的部分
```
## 引入的 package
```
    "@fortawesome/fontawesome-svg-core": "^1.2.35",
    "@fortawesome/free-solid-svg-icons": "^5.15.3",
    "@fortawesome/vue-fontawesome": "^2.0.2",
    以上是負責引入 fortawesome icon

    "sass-loader": "10.1.1",
    "node-sass": "5.0.0",
    以上是為了使用 scss 

    "lodash": "^4.17.21",
    以上是為了使用 cloneDeep(Object) 這個函數，目的是 deep copy Object

    另外引入新的字型，在 App.vue 的 style 部分
```

## 部署
```
此 project 部署至 Github Pages:
> - [連結](https://dawsonchang.github.io/drink-something/)
```

## Project setup
```
yarn install
```

### Compiles and hot-reloads for development
```
yarn serve
```

### Compiles and minifies for production
```
yarn build
```

### Lints and fixes files
```
yarn lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
