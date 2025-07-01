Serve per sincronizzare automaticamente il component e la vista, in entrambe le direzioni. Quando un valore nella vista (html) cambia, il modello viene aggiornato automaticamente, e viceversa.    
Combina sia il property binding (`[]`) sia l'event binding (`()`) in una sintassi unica (`[()]`).
##### Stesso Componente

```ts
import { formsModule } from '@angular/forms';

@NgModule({
	imports: [BrowserModule, FormsMoule],
	...
})
export class Component {
	nome: string = '';
}
```

```html
<input [(ngModel)]="nome" placeholder="Inserisci il nome..."/>
<p>Nome: {{nome}}!</p>
```

##### Tra due componenti (padre e figlio)

###### Con @Input e @Output

`ParentComponent.ts`:

```ts
export class ParentComponent {
  bindedValue: number = 0;
}
```

`ParentComponent.html`:

```html
<p>Value: {{bindedValue}}</p>
<app-children-component [(value)]="bindedValue"></app-children-component>
```

`ChildrenComponent.ts`:

```ts
import { Input, Output, EventEmitter } from '@angular/core';

export class ChildrenComponent {
  @Input() value: number = 0;
  @Output() valueChange = new EventEmitter<number>();

  // funzioni che fanno delle modifiche al valore
  increment() {
    this.value++;
    this.value.emit(this.value);
  }

  decrement() {
    this.value--;
    this.value.emit(this.value);
  }
}
```

`ChildrenComponent.html`:

```html
<button id="ngSubtractButton" (click)="decrement()"> - </button>
  <p>{{value}}</p>
<button id="ngAddButton" (click)="increment()"> + </button>
```

###### Con i signal

`ParentComponent.ts`:

```ts
export class ParentComponent {
  bindedValue: number = 0;
}
```

`ParentComponent.html`:

```html
<p>Value: {{bindedValue}}</p>
<app-children-component [(value)]="bindedValue"></app-children-component>
```

`ChildrenComponent.ts`:

```ts
import { Component, model } from '@angular/core';

export class ChildrenComponent {
  value = model<number>(0);

  // funzioni che fanno delle modifiche al valore
  updateCount(amount: number): void {
    this.value.update(val => val + amount); // oppure value.set(value() + amount);
  }
}
```

`ChildrenComponent.html`:

```html
<button id="ngSubtractButton" (click)="updateCount(-1)"> - </button>
  <p>{{value()}}</p>
<button id="ngAddButton" (click)="updateCount(+1)"> + </button>
```
