Gestione di un form con react.

`FormComponent.tsx`:

```tsx
import { useFormComponent } from './useFormComponent';

const FormComponent = () => {
	const { onSubmit } = useFormComponent(); // anche isValid per gestire gli errori
	
	render (
		<form onSubmit={onSubmit}>
		  <input type="text" id="username" name="username" required />
		  <input type="password" id="password" name="password" required />
		  <button type="submit">sign in</button>
		</form>
	);
}

export const FormComponent;
```

`useFormComponent.ts`:

```ts
import { useState } from 'react';
import { userLogin } from '../services/userService';

export const useSearchBar = () => {
	const [isValid, setisValid] = useState<boolean | null>(null);
	
	const onSubmit = async (e: React.FormEvent) => {
        e.preventDefault();

        setDataValid(null);

        const username = (document.getElementById('username') as HTMLInputElement).value;
        const password = (document.getElementById('password') as HTMLInputElement).value;

        // eventuali altre azioni per validare il form

        const res = await userLogin(username, password); // chiamata API

        if(!res){
            setIsValid(false);
        } else {
            setIsValid(true);
        }
    };

    return {
      onSubmit,
      isValid
    }
}
```

Metodo indiano più semplice per prendere i dati:

```ts
	const onSubmit = async (e: React.FormEvent) => {
        e.preventDefault();
        
        setDataValid(null);
        
        const form = e.target as HTMLFormElement;
        const formData = new FormData(form);
        const formDataObj = Object.fromEntries(formData.entries());
        
        // const formJSON = JSON.stringify(formDataObj) -> se necessario

        // eventuali altre azioni per validare il form

        // const res = await userLogin(formDataObj.username, formDataObj.password);
        // o meglio solo oggetto, poi gestire da service:
        const res = await userLogin(formDataObj);

        if(!res){
            setIsValid(false);
        } else {
            setIsValid(true);
        }
    };
```
