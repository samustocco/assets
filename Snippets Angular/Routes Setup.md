Creazione delle route:

`app.routes.ts`:

```ts
export const routes: Routes = [
    {path: '', component: HomeComponent},
    {path: 'home', component: HomeComponent },
    {path: 'page1', component: Page1Component },
    {path: 'page2', component: Page2Component},
    {path: '**', redirectTo: 'home' }
];
```

`app.html`:

```html
... componenti da tenere fuori le route
<main>
  <router-outlet /> <!-- qui vengono caicate le route -->
</main>
```

Utilizzo delle route:

`Navbar.html`:

```html
<ul class="nav">
    <li class="nav-item">
        <a routerLink="/" routerLinkActive="router-link-active">Home</a>
    </li>
    <li class="nav-item">
        <a routerLink="/page1">Page 1</a>
    </li>
</ul>
```

##### Route dinamiche:

`app.routes.ts`:

```ts
export const routes: Routes = [
    {path: 'page1/:id', component: Page1ComponentDetail },
];
```

Leggere il parametro dinamico:

`Page1ComponentDetail`:

```ts
import { Component, OnInit } from '@angular/core';
import { ActivatedRoute } from '@angular/router';

@Component({
  selector: 'app-page-1-component-detail',
  template: `<p>Detail ID: {{ id }}</p>`
})
export class Page1ComponentDetail implements OnInit {
  id!: string;

  constructor(private route: ActivatedRoute) {}

  ngOnInit(): void {
    this.route.paramMap.subscribe(params => {
      this.id = params.get('id')!;
    });
  }
}
```

Navigare tramite route dinamiche:

```html
<a routerLink="['/prodotti', prodotto.id]">Dettaglio</a>
```

##### Route annidate:

`app.routes.ts`:

```ts
export const routes: Routes = [
    {
      path: '', 
      component: HomeComponent,
      children: [
        { path: 'childRoute1', component: ChildComponent1 },
        { path: 'childRoute2', component: ChildComponent2 },
        { path: '', redirectTo: 'childRoute1', pathMatch: 'full' }
      ]
    }
];
```

Per renderizzare le route bisogna inserire il `router-outlet` nel parent.

```html
<h2>Home</h2>
<nav>
  <a routerLink="statistiche">Statistiche</a> |
  <a routerLink="impostazioni">Impostazioni</a>
</nav>
<router-outlet></router-outlet>
```
