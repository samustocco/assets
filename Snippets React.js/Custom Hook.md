Component.tsx

```tsx
import './Component.css';
import { useComponent } from './useComponent';

const Component = () => {

    const { myUseState, myFunction } = useComponent();  

    return (
        <>...</>
    );

} 

export default SearchBar;
```

Component.ts

```Ts
import { useState } from 'react';

export const useSearchBar = () => {

    const [myUseState, setmyUseState] = useState('');
    
    const myFunction = () => {
      ...
    }
    
    return {
      myUseState,
      myFunction
    }
}
```
