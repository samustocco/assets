`useEffect` viene eseguito subito dopo il render del componente, e quando una dipendenza si aggiorna. 

Sintassi:

```tsx
import { useEffect } from 'react';

const Component = () => {
    
    useEffect(() => {
        ...
    }, [dipendenze, ...]);
    
    return (
        ...
    );
}

export default ResultsPage;
```

Casi di esecuzione:

1. **Array vuoto**: eseguito al mount del componente (il primo render).

```tsx
    useEffect(() => {
        console.log('eseguito');
    }, []);
```

2. **Dipendenze presenti**: eseguito al cambio di valore della dipendenza.

```tsx
    useEffect(() => {
        console.log('${variabile} aggiornato');
    }, [variabile]);
```

3. **Senza array**: eseguito ad ogni render.

```tsx
    useEffect(() => {
        console.log('render avvenuto');
    });
```

###### Funzionalità aggiuntive di useEffect:

Cleanup di un effetto (per un interval, o un logout):

```tsx
useEffect(() => {
	const interval = setInterval(() => {
		...
	}, 1000);
	
	// si esegue solo all'unmount o se il valore dipendenza cambia
	return () => {
      clearInterval(interval);
    };
}, []);
```

Esecuzione solo al cambio di uno specifico parametro:

```tsx
useEffect(() => {
	if (variabile1){
		// codice da eseguire al cambio di variabile1
	}
	...
}, [variabile1, variabile2, ...]);
```
