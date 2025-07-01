
`ProviderComponent.tsx`:

```tsx
import { useState, createContext } from 'react';

export const UserContext = createContext();

const ProviderComponent = () => {
	const [user, setuser] = useState('username');
	
	return(
		<UserContext.Provider value={user}>
			{Children}
		</UserContext.Provider>
	);
}

export default ProviderComponent;
```

Utilizzare i valori nel context:

`ConsumerComponent.tsx`:

```tsx
import { useContext } from 'react';
import { UserContext } from '../ProviderComponent';

const ConsumerComponent = () => {
	const user = useContext(UserContext);
	
	return(
		<h3>{`Username: ${user}`}</h3>
	);
}

export default ConsumerComponent;
```

Applicare il context:

`App.tsx`:

```tsx
import ProviderComponent from '../contexts/ProviderComponent';

function App() {
	return(
		<>
		  <ProviderComponent>
		  ...
		  </ProviderComponent>
		</>
	);
}

export default App;
```
