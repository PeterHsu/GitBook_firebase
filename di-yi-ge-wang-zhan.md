# 第一個網站

## 建立專案

以下執行若有不成功, 就請用管理員身分執行

```
>ng new PeterFire --routing --style=scss
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

或修改package.json, "start": "ng serve --open"

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
>npm start
```

* 結束

按著Ctrl不放, 連按兩次C

## 部署

一、

在Firebase上建立新的專案, [https://console.firebase.google.com](#)

![](/assets/import.png)

二、

執行

```
>firebase init
```

第1/5的問題：Yes  
第2/5的問題：Hosting

![](/assets/import1.png)

第3/5的問題：選擇剛剛建立好的專案

![](/assets/import4.png)

第4/5的問題：dist  
第5/5的問題：Yes  
以下是完整的結果

![](/assets/import5.png)

三、

執行

```
>ng builde --prod --aot
```

或修改package.json, "build": "ng build --prod --aot"

```json
"scripts": {
    "ng": "ng",
    "start": "ng serve --open",
    "build": "ng build --prod --aot",
    "test": "ng test",
    "lint": "ng lint",
    "e2e": "ng e2e"
  },
```

執行

```
>npm run build
```

四、

執行

```
>firebase deploy
```

![](/assets/import6.png)

瀏覽 [https://peterfire-d933c.firebaseapp.com/](https://peterfire-d933c.firebaseapp.com/)

