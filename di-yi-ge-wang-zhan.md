# 第一個網站

## 建立專案

以下執行若有不成功, 就請用管理員身分執行

```
>ng new PeterFire --routing --style=scss
>cd PeterFire
>npm install firebase angularfire2 --save
```

## 測試專案

* 啟動測試的網站伺服器

```
>ng serve
```

或

```
>npm start
```

瀏覽

[http://localhost:4200/](http://localhost:4200/)

* 啟動後自動瀏覽

```
>ng serve --open
```

或修改package.json, 將"start"加上--open參數

```json
"scripts": {
    "ng": "ng",
    "start": "ng serve --open",
    "build": "ng build",
    "test": "ng test",
    "lint": "ng lint",
    "e2e": "ng e2e"
  },
```

執行

```
npm start
```

* 結束

按著Ctrl不放, 連按兩次C

## 部署

1. [https://console.firebase.google.com](#)

在Firebase上建立新的專案

![](/assets/import.png)

1. 執行

```
>firebase init
```

第1/3及1/3的問題

![](/assets/import1.png)

第3/3的問題,  選擇剛剛建立好的專案

![](/assets/import4.png)

第4/5及5/5的問題, 　

![](/assets/import5.png)

