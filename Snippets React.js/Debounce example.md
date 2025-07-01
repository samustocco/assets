Funzione di debounce:

```ts
const debounce = (fn, delay) => {
	let timeoutId;
	return (...args) => {
		clearTimeout(timeoutId);
		timeoutId = setTimeout(() => fn(...args), delay);
	}
}
```

Utilizzo in un input:

```tsx
const SearchInput = () => {
	const [query, setQuery] = useState('');
	
	const handleSearch = useCallback( // x non essere creata ad ogni render
		debounce((searchTerm) => {
			// api call per fetch dei risultati
		}, 500),
		[]
	)
	
	const handleChange = (e) => {
		setQuery(e.target.value);
		handleSearch(e.target.value);
	}
	
	return(
		<div>
		  <input
		    type="text"
		    value={query}
		    onChange={handleChange}
		    placeholder="search..."
		  />
		</div>
	)
}
```

Altre info: https://medium.com/@ignatovich.dm/debouncing-and-throttling-in-react-whats-the-difference-and-how-to-implement-them-0a500b649235
