Creare un service:

```shell
ng generate service nome-service
```

Per usare HTTP client:

`app.config.ts`:

```ts
...
import { provideHttpClient } from '@angular/common/http';

export const appConfig: ApplicationConfig = {
  providers: [
    ...
    provideHttpClient()

  ]
};
```

`nome-service.ts`:

```ts
import { HttpClient } from '@angular/common/http';

@Injectable({
  providedIn: 'root'
})

export class GenericService {
  private httpClient = inject(HttpClient);
  ...
}
```

##### Metodi HTTP:

GET

```ts
  private fetchData<T>(url: string, errorMsg:string) {
    return this.httpClient.get<T>(url).pipe(
      catchError((err) => {
        return throwError(() => new Error(errorMsg));
      })
    );
  }
```

GET by ID

```ts
  private fetchById<T>(url: string, id: number, errorMsg:string) {
    return this.httpClient.get<T>(`${url}/${id}`).pipe(
      catchError(() => {
        return throwError(() => new Error(errorMsg));
      })
    );
  }
```

POST

```ts
  private fetchPost<T>(url: string, body: any, errorMsg:string) {
    return this.httpClient.post<T>(url, body).pipe(
      catchError(() => {
        return throwError(() => new Error(errorMsg));
      })
    );
  }
```

##### Metodi specifici (si chiamano nei componenti):

Get

```ts
  public getSomething() {
    return this.fetchData<SomethingType[]>(`${this.baseUrl}/something`, 'Error fetching something');
  }
```

Get by ID

```ts
  public getSomethingById(id: number) {

    return this.fetchById<SomethingType>(`${this.baseUrl}/something`, id, 'Error fetching message by ID');

  }
```

Post

```ts
  public postSomething(payload: PayloadType) {
    return this.fetchPost<SomethingType>(`${this.baseUrl}/something`, payload, 'Error posting something');
  }
```

##### Utilizzo dei service

`component-name.ts`:

```ts
import { NomeService } from '../services/nome-service';

export class ComponentName {

  something: SomethingType | null = null; // o qualsiasi altra cosa da mandare

  private nomeService = inject(NomeService);

  onPostButtonClick() { // ngOnInit() in caso di get
    this.nomeService.postSomething(this.something).subscribe({
      next: (response) => {
        // codice se il post avviene con successo
      },
      error: (err) => {
        // codice se il post fallisce
        console.error(err);
      }
    });
  }
  
}
```
