<h1 align="center">
  <img src="https://camo.githubusercontent.com/8c13dc2618dbd7f76d1d574350b98fdee1335ce5/68747470733a2f2f726f636b6574736561742d63646e2e73332d73612d656173742d312e616d617a6f6e6177732e636f6d2f626f6f7463616d702d6865616465722e706e67" width="200px" />
</h1>

<h3 align="center">
  :rocket: [Bootcamp GoStack#10] Arquitetura Flux, Redux, Redux Saga.
</h3>

### Rodando na sua maquina:

1. Baixe o arquivo ***.ZIP***
2. `cd React-Native-Intro-master`
3. `yarn` para instalar as dependencias
4. `yarn start` para iniciar o servidor e abrirá automaticamente

# Arquitetura Flux

Manipular estados Globais de uma aplicaçāo de forma robusta e escalavel.

## Aula 01 - Criar projeto

Criamo um projeto ***ReactJS*** basico igual ensino no inicio da [parte 2 de react native](https://github.com/peguimasid/React-Part-2), e deixamos so um `Hello World` lá.

## Aula 02 - Configurando rotas

1. Dentro de `src` criamos um arquivo `routes.js`
2.`yarn add react-router-dom`
3. Criamos dentro de `src` uma pasta `pages` e dentro dela duas pastas: `Home` e `Cart`, cada uma com um arquivo `index.js` dentro.
4. Fazemos as config base de cada index:

```
import React from 'react';

export default function Home && Cart() {
  return <div />;
}
```

5. Vamos em `routes.js`:

```
import React from 'react';
import { Route, Switch } from 'react-router-dom';

import Home from './pages/Home';
import Cart from './pages/Cart';

export default function Routes() {
  return (
    <Switch>
      <Route path="/" exact component={Home} />
      <Route path="/cart" component={Cart} />
    </Switch>
  );
}
```

6. Depois em `src > App.js`:

```
import React from 'react';
import { BrowserRouter } from 'react-router-dom';

import Routes from './routes';

function App() {
  return (
    <BrowserRouter>
      <Routes />
    </BrowserRouter>
  );
}

export default App;
```

Nos nao colocamos o `<BrowserRouter>` dentro de `routes.js` pois como o nosso `<Header>` vai ser clicavel, nos precisamos dele ali em cima das `<Routes>` para ele poder fazer a navegaçāo.
