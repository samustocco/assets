Installazione

```bash
npm install react-router
```

Struttura file:

```
my-app/
├─ components/
├─ routes/
│  ├─ Home.tsx
│  ├─ Page1.tsx
│  ├─ Page2.tsx
├─ App.tsx
├─ ...
```

App.tsx

```tsx
import { BrowserRouter, Route, Routes } from 'react-router-dom';
import { Component ...} from './routes/...'; 

function App() {

return (
    <>
    <BrowserRouter>
      ... eventuali altri elementi fuori dalle routes (Header, Navbar, Footer...)
      <Routes>
        <Route path="/" element={<Component />} />
        <Route path="/path1" element={<Component />} />
        <Route path='/path2' element={<Component />} />
        <Route path='/path3' element={<Component />} />
        <Route path="*" element={<Component />} />
      </Routes>
    </BrowserRouter>
    </>
  )
}
  
export default App
```

Utilizzo:

```tsx
import { NavLink } from 'react-router-dom';

...

<NavLink to={'/path1'}>...</NavLink>
```

Esempio di Navbar:

```tsx
import { NavLink } from 'react-router-dom';

const Navigation = () => {
    return (
        <nav className="navigation">
            <NavLink to={'/results'} className={'nav-link'}>Results</NavLink>
            <NavLink to={'/page1'} className={'nav-link'}>Page 1</NavLink>
            <NavLink to={'/page2'} className={'nav-link'}>Page 2</NavLink>
        </nav>
    );
} 

export default Navigation;
```

##### Route dinamiche:

```tsx
return (
    <>
    <BrowserRouter>
      ... eventuali altri elementi fuori dalle routes
      <Routes>
        <Route path="/" element={<Component />} />
        <Route path="/pokemon" element={<PokemonPage />} />
        <Route path="/pokemon/:id" element={<PokemonDetail />} />
      </Routes>
    </BrowserRouter>
    </>
  )
```

Ottenere i parametri dall'url:

```tsx
import { useParams } from "react-router"; 

export default function PokemonDetail() { 
	let params = useParams(); 
	// params.id 
}
```

Navigare verso una route dinamica:

```tsx
return (
    <>
      <Link to={`pokemon/${id}`} />
    </>
  )
```

##### Route annidate:

```tsx
return (
    <>
    <BrowserRouter>
      ... eventuali altri elementi fuori dalle routes
      <Routes>
        <Route path="/" element={<Component />} />
        <Route path="/pokemon" element={<PokemonPage />} >
          <Route path=":id" element={<PokemonDetail />} />
        </Route>
      </Routes>
    </BrowserRouter>
    </>
  )
```

Il risultato sarà nell'url:

`/pokemon/1`

Per renderizzare le route annidate bisogna inserire il componente `Outlet` nel parent:

```tsx
import { Outlet } from "react-router"; 

export default function PokemonPage() { 
	return ( 
		<div> 
		  <h1>Pokemons</h1>  
		  <Outlet /> {/* sarà pokemon/1 ecc... */}
		</div> 
	);
}
```

Altre informazioni: https://reactrouter.com/start/declarative/routing#layout-routes
