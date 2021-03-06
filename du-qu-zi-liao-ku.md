# 讀取資料庫

## 安裝需要的套件

```
>npm install firebase angularfire2 --save
```

## 取得Firebase專案的資訊

1. 上 [https://console.firebase.google.com](https://console.firebase.google.com)
2. 進入PeterFire的專案
3. 進入\[將Firebase加入您的網路應用程式\]  
   ![](/assets/import10.png)

4. 會看到專案資訊, 等下程式裡會需要用到  
   ![](/assets/import11.png)

## 開發程式

### 設定Firebase參數

environment.ts

```js
export const environment = {
  production: false,
  firebase: {
    apiKey: 'AIzaSyClYV4rIXtXFI7xo9vq0UIc7mKOYdxG8V0',
    authDomain: 'peterfire-d933c.firebaseapp.com',
    databaseURL: 'https://peterfire-d933c.firebaseio.com',
    projectId: 'peterfire-d933c',
    storageBucket: 'peterfire-d933c.appspot.com',
    messagingSenderId: '673036642538'
  }
};
```

### 加入Firebase模組

app.module.ts

```js
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';

import { AppRoutingModule } from './app-routing.module';
import { AppComponent } from './app.component';

import { AngularFireModule } from 'angularfire2';
import { AngularFirestoreModule } from 'angularfire2/firestore';
import { environment } from '../environments/environment';

@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    AppRoutingModule,
    AngularFireModule.initializeApp(environment.firebase),
    AngularFirestoreModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

### 讀取資料

app.component.ts

```js
import { Component } from '@angular/core';
import { AngularFirestore } from 'angularfire2/firestore';
import { Observable } from 'rxjs/Observable';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.scss']
})
export class AppComponent {
  items: Observable<any[]>;
  constructor(db: AngularFirestore) {
    this.items = db.collection('items').valueChanges();
  }
}
```

### 畫面顯示

app.component.html

```html
<ul>
  <li *ngFor="let item of items | async">
    {{item.name}}
  </li>
</ul>
<router-outlet></router-outlet>
```

## 啟動資料庫

上Firebase, 啟動Cloud Firestore

![](/assets/import12.png)

選擇\[以測試模式啟動\]

![](/assets/import13.png)

建立資料

![](/assets/import14.png)

![](/assets/import15.png)

![](/assets/import16.png)

結果

![](/assets/import17.png)

## 測試

```
>ng serve
```

瀏覽 [http://localhost:4200/](http://localhost:4200/)

畫面如下

![](/assets/import18.png)

## 佈署

### 設定Firebase正式環境的參數

environment.prod.ts, 內容和environment.ts一樣

```js
export const environment = {
  production: false,
  firebase: {
    apiKey: 'AIzaSyClYV4rIXtXFI7xo9vq0UIc7mKOYdxG8V0',
    authDomain: 'peterfire-d933c.firebaseapp.com',
    databaseURL: 'https://peterfire-d933c.firebaseio.com',
    projectId: 'peterfire-d933c',
    storageBucket: 'peterfire-d933c.appspot.com',
    messagingSenderId: '673036642538'
  }
};
```

### 建置

```
>ng build --prod --aot
>firebase deploy
```

瀏覽 [https://peterfire-d933c.firebaseapp.com/](https://peterfire-d933c.firebaseapp.com/)

## 測試

網頁不要關, 到firebase console改掉name, 畫面應該要自動更新

![](/assets/import19.png)

