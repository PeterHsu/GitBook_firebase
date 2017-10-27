# 我的第一個網站

## 建立專案

以下執行若有不成功, 就請用管理員身分執行

```
>ng new PeterFire --routing --style=scss
>cd PeterFire
>npm install firebase angularfire2 --save

```

## 測試

app.component.ts

```
import { Component } from '@angular/core';
import { Observable } from 'rxjs/Observable';
import { AngularFireAuth } from 'angularfire2/auth';
import * as firebase from 'firebase/app';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.scss']
})
export class AppComponent {
  constructor(public afAuth: AngularFireAuth) {
  }
  login() {
    this.afAuth.auth.signInWithPopup(new firebase.auth.GoogleAuthProvider());
  }
  logout() {
    this.afAuth.auth.signOut();
  }
}
```

app.component.html

```
<div *ngIf="afAuth.authState | async; let user; else showLogin">
  <h1>Hello {{ user.displayName }}!</h1>
  <button (click)="logout()">Logout</button>
</div>
<ng-template #showLogin>
  <p>Please login.</p>
  <button (click)="login()">Login with Google</button>
</ng-template>
```

app.module.ts

```
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';

import { AppRoutingModule } from './app-routing.module';
import { AppComponent } from './app.component';

import { AngularFireModule } from 'angularfire2';
import { AngularFireDatabaseModule, AngularFireDatabase } from 'angularfire2/database';
import { AngularFireAuthModule } from 'angularfire2/auth';

export const firebaseConfig = {
  apiKey: "AIzaSyDhLusfoLjudWciZx_8tOFVcEBfzbNHYPg",
  authDomain: "lab01-2b420.firebaseapp.com",
  databaseURL: "https://lab01-2b420.firebaseio.com",
  projectId: "lab01-2b420",
  storageBucket: "lab01-2b420.appspot.com",
  messagingSenderId: "732164315180"
};

@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    AppRoutingModule,
    AngularFireModule.initializeApp(firebaseConfig),
    AngularFireDatabaseModule,
    AngularFireAuthModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```



