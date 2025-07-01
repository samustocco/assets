##### Template Driven Forms

Con i template driven forms è possibile costruire e validare form nella vista (HTML) del componente, utilizzando il two-way data binding per comunicare con il controller (TS).

`Component.html`

```html
<form #userForm="ngForm" class="template-form" (submit)="onSubmit(userForm)">
    <div>
        <label for="username">Username</label>
        <input 
          type="text" 
          id="username" 
          name="username" 
          [(ngModel)]="user.username"
          #username="ngModel"
          required
        />
    </div>
    <div>
        <label for="email">Email</label>
        <input 
          type="email" 
          id="email" 
          name="email" 
          [(ngModel)]="user.email" 
          #email="ngModel" 
          email 
          required
        />
    </div>
    <div>
        <label for="password">Password</label>
        <input 
          type="password" 
          id="password" 
          name="password" 
          [(ngModel)]="user.password" 
          #password="ngModel" 
          required 
          minlength="6"
        />
    </div>
    <div>
        <h5>Gender</h5>
        <label>
            <input 
              type="radio" 
              name="gender" 
              value="male" 
              [(ngModel)]="user.gender" 
              #gender="ngModel" 
              required
            />
            M
        </label>
        <label>
            <input 
              type="radio" 
              name="gender" 
              value="female" 
              [(ngModel)]="user.gender" 
              #gender="ngModel"  
              required
            />
            F
        </label>
        <label>
            <input 
              type="radio" 
              name="gender" 
              value="other" 
              [(ngModel)]="user.gender" 
              #gender="ngModel" 
              required
            />
            Other
        </label>
    </div>
    <div>
        <label for="acceptTerms">I accept the terms & conditions</label>
        <input 
          type="checkbox" 
          id="acceptTerms" 
          name="acceptTerms" 
          [(ngModel)]="user.acceptTerms" 
          #acceptTerms="ngModel" 
          required
        />
    </div>
    <button type="submit" [disabled]="!userForm.valid">Submit</button>
    <button type="reset">Reset</button>
</form>
```

`Component.ts`:

```ts
import { FormsModule } from '@angular/forms';
import { type UserInfo } from '../user-info.model';

...
export class TemplateForms {

  // I dati in questo oggetto si aggiornano bidirezionalmente
  user: UserInfo = {
    username: 'mattiaverdi99',
    email: '',
    password: '',
    gender: '',
    acceptTerms: false
  };

  onSubmit(form: any) {
    if (form.valid) {
      // form.value per accedere ai dati
    }
  }
}
```

###### Validazione:

Messaggio di feedback (se il campo è invalido):

```html
@if(username.invalid && (username.dirty || username.touched)) {
	<div class="error">Username is required.</div>
}
```

##### Reactive Forms

I reactive form utilizzano un approccio a modello per gestire gli input e la validazione. Il modello è definito nel controller, e il template serve solo come "presentazione".

`Component.html`

```html
<form [formGroup]="userForm" (submit)="onSubmit()">
    <div>
        <label for="name">Username:</label>
        <input type="text" id="name" formControlName="username">
    </div>
    <div>
        <label for="email">Email:</label>
        <input type="email" id="email" formControlName="email">
    </div>
    <div>
        <label for="password">Password:</label>
        <input type="password" id="password" formControlName="password">
    </div>
    <div>
        <label>Gender:</label>
        <label>
            <input type="radio" value="male" formControlName="gender">
            M
        </label>
        <label>
            <input type="radio" value="female" formControlName="gender">
            F
        </label>
        <label>
            <input type="radio" value="other" formControlName="gender">
            Other
        </label>
    </div>
    <div>
        <label for="acceptTerms">I accept the terms & conditions</label>
        <input type="checkbox" id="acceptTerms" formControlName="acceptTerms">
    </div>
    <button type="submit" [disabled]="userForm.invalid">Submit</button>
    <button type="reset" (click)="userForm.reset()">Reset</button>
</form>
```

`Component.ts`

```ts
import { FormControl, FormGroup, ReactiveFormsModule, Validators, ValidatorFn, AbstractControl, ValidationErrors } from '@angular/forms';

...

export class ReactiveForms {
  submitted: boolean = false;
  
  // modello del form
  userForm: FormGroup = new FormGroup({
    username: new FormControl(''),
    email: new FormControl(''),
    password: new FormControl(''),
    gender: new FormControl(''),
    acceptTerms: new FormControl(false)  
  });

  // getter per accedere ai campi del form nel template
  get username() {
    return this.userForm.get('username');
  }

  get email() {
    return this.userForm.get('email');
  }

  get password() {
    return this.userForm.get('password');
  }
  
  get gender() {
    return this.userForm.get('gender');
  }

  get acceptTerms() {
    return this.userForm.get('acceptTerms');
  }

  // on submit funcion
  onSubmit(): void {
    if (this.userForm.valid) {;
      // this.userForm.value per accedere ai dati
    }
  }
}
```

Funzione per aggiornare un campo lato controller:

```ts
  updateUsername(): void {
    this.userForm.patchValue({
      username: 'newUsername'
    });
  }
```

Validazione:

La validazione viene fatta nel controller, a differenza dei template driven form.

```ts
  userForm: FormGroup = new FormGroup({
    username: new FormControl('', [
      Validators.required,
      Validators.minLength(4),
      this.customRegExValidator(/bober/i), // <-- custom validator.
    ]),
    email: new FormControl('', [
      Validators.required,
      Validators.email,
    ]),
    password: new FormControl('', [
      Validators.required,
      Validators.minLength(6),
    ]),
    gender: new FormControl('', [
      Validators.required,
    ]),
    acceptTerms: new FormControl(false, [
      Validators.requiredTrue
    ])
  });
```

Custom validator:

```ts
  // custom vaiddator function to test a RegEx
  customRegExValidator(regExp: RegExp): ValidatorFn {
    return (control: AbstractControl): ValidationErrors | null => {
      const valid = regExp.test(control.value);
      return valid ? { customRegEx: { value: control.value } } : null;
    };
  }
```

Messaggio di feedback (se il campo non è valido) nel template:

```jsx
<div>
    <label for="name">Username:</label>
    <input type="text" id="name" formControlName="username">
    @if(username?.invalid && (username?.dirty || username?.touched)) {
        @if(username?.hasError('required')) {
            <div class="error">Username is required.</div>
        }
        @if(username?.hasError('minlength')) {
            <div class="error">Username must be at least 3 characters long.</div>
        }
        @if(username?.hasError('customRegEx')) {
            <div class="error">Banned username</div>
        }
    }
</div>
```

Con i reactive form è possibile definire più semplicemente errori specifici per ogni input, controllando se un errore specifico è presente nel FormControl.
