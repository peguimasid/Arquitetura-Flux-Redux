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

<h3 align="center">A partir da aula 09 começamos <strong>Redux</strong></h3>

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

## Aula 03 - Estilos globais

1. Dentro de `src` criar uma pasta `styles` com um arquivo `global.js`
2. `yarn add styled-components`
3. `global.js`:

```
import { createGlobalStyle } from 'styled-components';

import background from '../assets/images/background.svg';

export default createGlobalStyle`
@import url('https://fonts.googleapis.com/css?family=Roboto:400,700&display=swap');
  * {
    margin: 0;
    padding: 0;
    outline: 0;
    box-sizing: border-box;
  }

  body {
    background: #1f1f1f url(${background}) no-repeat center top;
    -webkit-font-smoothing: antialiased;
  }

  body, input, button {
    font: 14px Roboto, sans-serif;
  }

  #root {
    max-width: 1020px;
    margin: 0 auto;
    padding: 0 20px 50px;
  }

  button {
    cursor: pointer;
  }
`;
```
4. Vamos em `src > App.js`:

```
import React from 'react';
import { BrowserRouter } from 'react-router-dom';

* import GlobalStyle from './styles/global';
import Routes from './routes';

function App() {
  return (
    <BrowserRouter>
      <Routes />
  *    <GlobalStyle />
    </BrowserRouter>
  );
}

export default App;
```

E nossos estilos serao aplicados em todas as paginas

## Aula 04 - Criando Header

1. Dentro da pasta `src` vamos criar uma pasta `components`
2. `yarn add react-icons`
3. Dentro de dela criamos uma pasta `Header` com um arquivo `index.js` e um `styles.js`.

`index.js`:

```
import React from 'react';
import { Link } from 'react-router-dom';

import { MdShoppingBasket } from 'react-icons/md';

import { Container, Cart } from './styles';

import logo from '../../assets/images/logo.svg';

export default function Header() {
  return (
    <Container>
      <Link to="/">
        <img src={logo} alt="Rocketshoes" />
      </Link>

      <Cart to="/cart">
        <div>
          <strong>Meu carrinho</strong>
          <span>3 itens</span>
        </div>
        <MdShoppingBasket size={36} color="#fff" />
      </Cart>
    </Container>
  );
}
```

`styles.js`:

```
import styled from 'styled-components';
import { Link } from 'react-router-dom';

export const Container = styled.header`
  display: flex;
  justify-content: space-between;
  margin: 50px 0;
`;

export const Cart = styled(Link)`
  display: flex;
  align-items: center;
  text-decoration: none;
  transition: opacity 0.2s;

  &:hover {
    opacity: 0.7;
  }

  div {
    text-align: right;
    margin-right: 10px;

    strong {
      display: block;
      color: #fff;
    }

    span {
      font-size: 12px;
      color: #999;
    }
  }
`;
```
4. Em `src > App.js` colocamos assim:

```
...
import Header from './components/Header';
...
return (
    <BrowserRouter>
  **    <Header />
      <Routes />
      <GlobalStyle />
    </BrowserRouter>
  );
```

## Aula 05 - Estilizaçao da Home

1. Dentro de `src > Home` vamos criar um arquivo `styles.js`
2. Vamos fazer agora as duas paginas:

`Home > index.js`:

```
import React from 'react';
import { MdAddShoppingCart } from 'react-icons/md';

import { ProductList } from './styles';

export default function Home() {
  return (
    <ProductList>
      <li>
        <img
          src="https://static.netshoes.com.br/produtos/tenis-de-caminhada-leve-confortavel/06/E74-0492-006/E74-0492-006_zoom2.jpg?ts=1579006188&ims=326x"
          alt="Tênis"
        />
        <strong>Tênis muito legal</strong>
        <span>R$129,90</span>

        <button type="button">
          <div>
            <MdAddShoppingCart size={16} color="#fff" /> 3
          </div>

          <span>ADICIONAR AO CARRINHO</span>
        </button>
      </li>
      <li>
        <img
          src="https://static.netshoes.com.br/produtos/tenis-de-caminhada-leve-confortavel/06/E74-0492-006/E74-0492-006_zoom2.jpg?ts=1579006188&ims=326x"
          alt="Tênis"
        />
        <strong>Tênis muito legal</strong>
        <span>R$129,90</span>

        <button type="button">
          <div>
            <MdAddShoppingCart size={16} color="#fff" /> 3
          </div>

          <span>ADICIONAR AO CARRINHO</span>
        </button>
      </li>
  </ProductList>
  );
}
```

`Home > styles.js`:

```
import styled from 'styled-components';
import { darken } from 'polished';

export const ProductList = styled.ul`
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 20px;
  list-style: none;

  li {
    display: flex;
    flex-direction: column;
    background: #fff;
    border-radius: 4px;
    padding: 20px;

    img {
      align-self: center;
      max-width: 250px;
    }

    > strong {
      font-size: 16px;
      line-height: 20px;
      color: #333;
      margin-top: 5px;
    }

    > span {
      font-size: 21px;
      font-weight: bold;
      margin: 5px 0 20px;
    }

    button {
      background: #245edb;
      color: #fff;
      border: 0;
      border-radius: 4px;
      overflow: hidden;
      margin-top: auto;

      display: flex;
      align-items: center;
      transition: 0.2s;

      &:hover {
        background: ${darken(0.02, '#245ebd')};
      }

      div {
        display: flex;
        align-items: center;
        padding: 12px;
        background: rgba(0, 0, 0, 0.1);

        svg {
          margin-right: 5px;
        }
      }

      span {
        flex: 1;
        text-align: center;
      }
    }
  }
`;

```
## Aula 06 - Estilizaçāo do Carrinho

`Cart > index.js`:

```
import React from 'react';
import {
  MdRemoveCircleOutline,
  MdAddCircleOutline,
  MdDelete,
} from 'react-icons/md';

import { Container, ProductTable, Total } from './styles';

export default function Home() {
  return (
    <Container>
      <ProductTable>
        <thead>
          <tr>
            <th>PRODUTO</th>
            <th>QTD</th>
            <th>SUBTOTAL</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>
              <img
                src="https://static.netshoes.com.br/produtos/tenis-de-caminhada-leve-confortavel/06/E74-0492-006/E74-0492-006_zoom2.jpg?ts=1579006188&ims=326x"
                alt="Tênis"
              />
            </td>
            <td>
              <strong>Tênis muito massa</strong>
              <span>R$129,90</span>
            </td>
            <td>
              <div>
                <button type="button">
                  <MdRemoveCircleOutline size={20} color="#245edb" />
                </button>
                <input type="number" readOnly value={2} />
                <button type="button">
                  <MdAddCircleOutline size={20} color="#245edb" />
                </button>
              </div>
            </td>
            <td>
              <strong>R$258,80</strong>
            </td>
            <td>
              <button type="button">
                <MdDelete size={20} color="#245edb" />
              </button>
            </td>
          </tr>
        </tbody>
      </ProductTable>

      <footer>
        <button type="button">Finalizar Pedido</button>

        <Total>
          <span>TOTAL</span>
          <strong>R$1920,90</strong>
        </Total>
      </footer>
    </Container>
  );
}
```

`Cart > styles.js`:

```
import styled from 'styled-components';
import { darken } from 'polished';

export const Container = styled.div`
  padding: 30px;
  background: #fff;
  border-radius: 4px;

  footer {
    margin-top: 30px;
    display: flex;
    justify-content: space-between;
    align-items: center;

    button {
      background: #245edb;
      color: #fff;
      border: 0;
      border-radius: 4px;
      padding: 12px 20px;
      text-transform: uppercase;
      transition: 0.2s;

      &:hover {
        background: ${darken(0.05, '#245edb')};
      }
    }
  }
`;

export const ProductTable = styled.table`
  width: 100%;

  thead th {
    color: #999;
    text-align: left;
    padding: 12px;
  }

  tbody td {
    padding: 12px;
    border-bottom: 1px solid #eee;
  }

  img {
    height: 100px;
  }

  strong {
    color: #333;
    display: block;
  }

  span {
    display: block;
    margin-top: 5px;
    font-size: 18px;
    font-weight: bold;
  }

  div {
    display: flex;
    align-items: center;

    input {
      border: 1px solid #ddd;
      border-radius: 4px;
      color: #666;
      padding: 6px;
      width: 50px;
    }
  }

  button {
    background: none;
    border: 0;
    padding: 6px;
  }
`;

export const Total = styled.div`
  display: flex;
  align-items: baseline;

  span {
    color: #999;
    font-weight: bold;
  }

  strong {
    font-size: 26px;
    margin-left: 5px;
  }
`;
```

## Aula 07 - Configurando API

Vamos configurar uma api fake com o ***JSON-Server*** e buscar dados dela.

1. `yarn global add json-server`
2. [Baixar o arquivo](https://skylab.rocketseat.com.br/api/files/1581084444037-attachment.json) e salvar como `server.json` na raiz da aplicaçāo.
3. `yarn add axios`
4. Criar dentro de `src` uma pasta `services` e dentro um arquivo `api.js`

`api.js`:

```
import axios from 'axios';

const api = axios.create({
  baseURL: 'http://localhost:3333',
});

export default api;
```

5. Para rodar a ***api*** é só rodar:

`json-server server.json -p 3333` -> Rodar uma unica vez.
`json-server server.json -p 3333 -w` -> Rodar ouvindo mudancas no arquivo.

## Aula 08 - Buscando produtos da API

Vamos buscar os dados da nossa API e passar la pra home onde estao os produtos.

1. Vamos em `pages > Home > index.js`

```
import React, { Component } from 'react';
import { MdAddShoppingCart } from 'react-icons/md';
import { formatPrice } from '../../util/format';
 * import api from '../../services/api';

import { ProductList } from './styles';

export default class Home extends Component {
 *   state = {
 *     products: [],
 *   };

  *  async componentDidMount() {
  *    const response = await api.get('products');
  *
  *    const data = response.data.map((product) => ({
  *      ...product,
  *      priceFormatted: formatPrice(product.price),
  *    }));

   *   this.setState({ products: data });
  }

 *   render() {
    const { products } = this.state;

    return (
  *      <ProductList>
  *        {products.map((product) => (
  *          <li key={product.id}>
  *            <img src={product.image} alt={product.title} />
  *            <strong>{product.title}</strong>
  *            <span>{product.priceFormatted}</span>
  *
  *            <button type="button">
  *              <div>
  *                <MdAddShoppingCart size={16} color="#fff" /> 3
  *              </div>
  *
  *              <span>ADICIONAR AO CARRINHO</span>
  *            </button>
  *          </li>
  *        ))}
      </ProductList>
    );
  }
}
```
## Aula 09 - Configurando o Redux

Vamos nessa aula começar a configurar o ***Redux*** para usar em nossa aplicaçāo.

1. `yarn add redux react-redux`
2. Dentro de `src` criamos uma pasta `store` de dentro dela um arquivo `index.js`

`index.js`:

```
import { createStore } from 'redux';

const store = createStore();

export default store;
```
3. Depois disso vamos em `src > App.js` e passamos uma tag `<Provider>` por volta de todas as nossas rotas, o que vai fazer com que esse estado global fique disponive pra todos os componentes da aplicacao

```
...
import { Provider } from 'react-redux';
...
import store from './store';
...
function App() {
  return (
    <Provider store={store}>
      <BrowserRouter>
        <Header />
        <Routes />
        <GlobalStyle />
      </BrowserRouter>
    </Provider>
  );
}
```

A principio vai dar erro pois nao podemos criar um store sem nehum reducer, e é isso que vamos fazer agora.

4. Vamos em `src > store > index.js` e agora vamos adicionar isso:

```
import { createStore } from 'redux';

* function cart() {
*   return [];
* }

const store = createStore(cart);
                          ****
export default store;
```
como nao é legal mastermos os reducer's dentro do mesmo local que o store vamso fazer o seguinte.

5. dentro de `src > store` criamos uma pasta `modules` e dentro dela outra pasta chamada `cart` e dentro dela um arquivo chamado `reducer.js`

retiramos a `function cart()` de dentro do store e passamos dentro desse `reducer`, ficando assim:

`reducer.js`:

```
export default function cart() {
  return [];
}
```

`src > store > index.js`:

```
import { createStore } from 'redux';

import reducer from './modules/cart/reducer';

const store = createStore(reducer);

export default store;
```
Mas podemos tambem podemos ter mais de um reducer dentro do nosso store, e para lidar com esse tipo de caso vamos fazer o seguinte.

6. Vamos em `store > modules` e criamos um arquivo chamado `rootReducer.js`

`rootReducer`:

```
import { combineReducers } from 'redux';

import cart from './cart/reducer';
// import user from './user/reducer';

export default combineReducers({
  cart,
  // user,
});
```
Ai podemos criar quantos reducer's quisermos e passarmos ele dentro do `combineReducers`

Agora voltamos la em `store > index.js` e passamos assim:

```
import { createStore } from 'redux';

import rootReducer from './modules/rootReducer';

const store = createStore(rootReducer);

export default store;
```
agora temos a configuracao do ***Redux*** pronta, e a partir da proxima aula vamos começar a passar dados para dentro do nosso estado global `cart` que criamos la dentrode `modules > cart > reducer.js`

## Aula 10 - Adicionando ao carrinho

Vamos adicionar itens ao carrinho utlizando o ***Redux***

1. Vamos no componente que tem o botao de adicionar ao carrinho: `pages > Home > index.js`:

```
...
import { connect } from 'react-redux';
...
```

depois mudamos o `export default class Home extends Component { ...` para:

`class Home extends Component {...`

e passar o `export default` la para o final assim:

`export default connect()(Home);`

assim o Redux vai passar a ter acesso aos dados do nosso componente.

2. vamos passar uma funçāo para o nosso botāo de ***Adicionar ao carrinho*** passando o produto como parametro.

```
<button
  type="button"
  * onClick={() => this.handleAddProduct(product)}
>
```

3. Agora fora do `render()` criamos a funçāo que passamos:

```
handleAddProduct = (product) => {
    const { dispatch } = this.props;

    dispatch({
      type: 'ADD_TO_CART',
      product,
    });
  };
```
4. Agora vamos em `store > modules > cart > reducer.js` e o que estava assim:

```
export default function cart() {
  return [];
}
```

vai ficar assim:

```
export default function cart(state = [], action) {
  switch (action.type) {
    case 'ADD_TO_CART':
      return [...state, action.product];
    default:
      return state;
  }
}
```

Por padrao todas as actions que acontecem os reducer's ouvem e armazenam, entao passamos o metodo `switch` ali para verificar se aquele tipo de action é `ADD_TO_CART` se for ele vai copiar todos os dados que ja temos no estado e passar o novo, caso contrario, ele so vai retornar o estado.

5. Vamos agora em `src > components > Home > index.js` e fazemos o seguinte:

```
...
import { connect } from 'react-redux';
...
```
retiramos o `export default` e passamo no final igual fizemos no passo ***1***, e passamos o nosso Header assim agora:

```
function Header({ cartSize }) {
                  ********
  return (
    <Container>
      <Link to="/">
        <img src={logo} alt="Rocketshoes" />
      </Link>

      <Cart to="/cart">
        <div>
          <strong>Meu carrinho</strong>
          <span>{cartSize} itens</span>
                 ********
        </div>
        <MdShoppingBasket size={36} color="#fff" />
      </Cart>
    </Container>
  );
}

* export default connect((state) => ({
*   cartSize: state.cart.length, // nome que passamos no rootReducer
* }))(Header);
```
com isso ao clicarmos em um botao de adicionar ao carrinho ele vai adicionar o produto ao estado `cart` e mudar o numero que temo la mostrando a quantidade de itens que temo no carrinho (`2 itens`).
