##### Installazione

```shell
cd [nome cartella]

npm -v

node -v

npm i -g @angular/cli

ng --version
```

Problema Execution Policy:

- Eseguire powershell come admin

```shell
Set-ExecutionPolicy

> unrestricted

> yes to all
```

Se non c'è il secondo prompt:

```shell
> Set-ExecutionPolicy Unrestricted -Scope Process;

> Set-ExecutionPolicy Unrestricted -Scope CurrentUser;

> Set-ExecutionPolicy Unrestricted -Scope LocalMachine;
```

##### Comandi Angular CLI

> Nuovo progetto:
   `ng new [nome progetto]`

> Component:
   `ng g c [nome component]`

> Service:
   `ng g service [nome service]`

> Dev server:
   `ng serve -o`

> Build:
   `ng build`
