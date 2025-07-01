Installation:

```shell
npm install tailwindcss @tailwindcss/vite
```

Configuration: 

`vite.config.ts:`

```ts
import { defineConfig } from 'vite';
import tailwindcss from '@tailwindcss/vite';

export default defineConfig({ 
	plugins: [ 
		tailwindcss(), 
	],
})
```

`index.css`

```css
@import "tailwindcss";

...
```

Usage:

*Come bootstrap, mettere le classi nei tag tsx*:

```tsx
const Component = () => {
    return (
        <nav className="flex align-center px-8 py-2 gap-4 bg-gray-800">
            <a href="" className={'text-white hover:underline'}>Results Page</a>
            <a href="" className={'text-white hover:underline'}>Page 1</a>
            <a href="" className={'text-white hover:underline'}>Page 2</a>
        </nav>
    );
}
```
