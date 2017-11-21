# 建立範例

## 目標

依Angular官方的Tutorial建立範例

資料庫

依範例資料加入資料庫

```js
export const HEROES: Hero[] = [
  { id: 11, name: 'Mr. Nice' },
  { id: 12, name: 'Narco' },
  { id: 13, name: 'Bombasto' },
  { id: 14, name: 'Celeritas' },
  { id: 15, name: 'Magneta' },
  { id: 16, name: 'RubberMan' },
  { id: 17, name: 'Dynama' },
  { id: 18, name: 'Dr IQ' },
  { id: 19, name: 'Magma' },
  { id: 20, name: 'Tornado' }
];
```

![](/assets/import31.png)

## 新增程式

```
>ng g class hero
>ng g service hero
>ng g component dashboard
```

## 程式碼

hero.ts

```js
export class Hero {
    id: number;
    name: string;
}
```

hero.service.ts

```js
import { Injectable } from '@angular/core';
import { AngularFirestore } from 'angularfire2/firestore';
import { Observable } from 'rxjs/Observable';
import { Hero } from './hero';

@Injectable()
export class HeroService {

  constructor(private db: AngularFirestore) { }

  getHeroes(): Observable<Hero[]> {
    return this.db.collection<Hero>('hero').valueChanges();
  }
  getHeroesWithID(): Observable<Array<Hero>> {
    return this.db.collection<Hero>('hero').snapshotChanges().map(actions => {
      return actions.map(action => {
        const data = action.payload.doc.data() as Hero;
        data.id = +action.payload.doc.id;
        return data;
      });
    });
  }
}
```

dashboard.component.ts

```js
import { Component, OnInit } from '@angular/core';
import { Observable } from 'rxjs/Observable';
import { HeroService } from '../hero.service';
import { Hero } from '../hero';

@Component({
  selector: 'app-dashboard',
  templateUrl: './dashboard.component.html',
  styleUrls: ['./dashboard.component.scss']
})
export class DashboardComponent implements OnInit {
  heroes: Observable<Hero[]>;
  constructor(private heroService: HeroService) {
  }
  ngOnInit() {
    this.getHeroes();
  }
  getHeroes(): void {
    // this.heroes = this.heroService.getHeroes();
    this.heroes = this.heroService.getHeroesWithID();
  }
}
```

app-routing.module.ts

```js
import { NgModule } from '@angular/core';
import { Routes, RouterModule } from '@angular/router';
import { DashboardComponent } from './dashboard/dashboard.component';

const routes: Routes = [
  { path: '', redirectTo: '/dashboard', pathMatch: 'full' },
  { path: 'dashboard', component: DashboardComponent }
];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule { }
```

app.component.ts

```js
import { Component} from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.scss']
})
export class AppComponent {
  title = 'Tour of Heroes';
}
```

## 加上bootstrap

```
>npm install bootstrap@4.0.0-beta.2
```

## 程式碼

styles.scss

```scss
@import "~bootstrap/scss/bootstrap";
```

app.component.html

```html
<div class="container">
  <h1>{{title}}</h1>
  <nav class="nav nav-pills">
    <a class="nav-item nav-link active" routerLink="/dashboard">Dashboard</a>
    <a class="nav-item nav-link" routerLink="/heroes">Heroes</a>
  </nav>
  <router-outlet></router-outlet>
</div>
```

dashboard.component.html

```html
<div class="row">
  <div class="col text-md-center">
    <h3>Top Heroes</h3>
  </div>
</div>
<div class="row">
  <div class="col-md-3" *ngFor="let hero of heroes | async">
    <div class="card text-white bg-success mb-3" style="width: 10rem;">
      <div class="card-body">
        <h4>{{hero.name}}</h4>
      </div>
    </div>
  </div>
</div>
```



