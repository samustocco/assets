##### Metodi HTTP

`SomethingService.ts`:

GET

```ts
export const getAllSomethings = async () => {
    try {
        const response = await fetch(`url...`, {
            method: 'GET',
            headers: {
                'Content-Type': 'application/json', // o altro se necessario
            },
        });
        if (!response.ok) {
            throw new Error(`HTTP error! status: ${response.status}`);
        }

        const data = await response.json();

        return data;
    } catch (error) {
        console.error('Error in ... API:', error);
        return null;
    }
};
```

GET by ID

```ts
export const getSomethingById = async (param: type) => {
    try {
        const response = await fetch(`url.../${param}`, {
            method: 'GET',
            headers: {
                'Content-Type': 'application/json', // o altro se necessario
            },
        });
        if (!response.ok) {
            throw new Error(`HTTP error! status: ${response.status}`);
        }

        const data = await response.json();

        return data;
    } catch (error) {
        console.error('Error in ... API:', error);
        return null;
    }
};
```

POST

```ts
export const postSomething = async (payload: type) => { // o più param
    try {
        const response = await fetch(`url...`, {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json', // o altro se necessario
            },
            body: JSON.stringify(payload),            }
        });
        if (!response.ok) {
            throw new Error(`HTTP error! status: ${response.status}`);
        }

        return true;
    } catch (error) {
        console.error('Error in ... API:', error);
        return null;
    }
};
```

##### Utilizzo dei service

`useComponentPage.ts`:

```ts
import { getSomething } from '../services/SomethingService';
import { type Something as SomethingType } from '../Something/Something.model';

export const useComponentPage = () => {
    // const [isLoading, setIsLoading] = useState(true);
    // const [SomethingID, setSomethingID] = useState<Something | null>(null);

    const fetchSomething = async () => {
        const response = await getSomething();
        if (response) {
            // se la chiamata ha successo...
            // setIsLoading(false);
        }
    };

    // per fare eseguire la chiamata al mount del component
    useEffect(() => {
        fetchSomething();
    }, []);
```
