Sono il modo più semplice per passare dei dati da un componente padre a un children in React.
Le props sono **Immutabili**.
##### Come passare le props

I function component di React accettano solo un oggetto come parametro: **props**. 

```tsx
const ChildrenComponent = (props) => {
  ...
}
```

Le props devono essere tipizzate. Si possono dichiarare e utilizzare in due modi nel children:

```tsx
interface ChildrenComponentProps {
  val: number;
  func: (param: number) => void;
}
// passa le props tramite un oggetto unico e le destruttura nel componente
const ChildrenComponent = (props: ChildrenComponentProps) => {
  const { val, func } = props;
  ...
}
```

```tsx
// passa le props esplicitate nell'ogetto
const ChildrenComponent = ( { val: number, func: (param: number) => void } ) => {
  // si possono usare normalmente val e func
  ...
}
```

Le props si devono sempre passare da un componente parent:

```tsx
const ParentComponent = () => {
  const [baseValue, setBaseValue] = useState(0);

  const randomFn = () => {
        console.log('This is a random function that does nothing');
    }
  
  return (
    <ChildrenComponent value={baseValue} func={randomFn} />
  );
}
```

##### Tipi di props

Impostare un valore di default:

```
```

Props opzionali.

```
```

Passare le props con l'operatore spread:

```
```

Passare ReactNode come props:

```
```
