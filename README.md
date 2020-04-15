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

export default function Cart() {
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

### O que fizemos:

1. ***Home***: Conectamos ele com o redux e disparamos as `actions` com o `dispatch`
2. ***Reducer***: Fizemos o reducer ouvir somente as action do tipo `ADD_TO_CART` e armazenamos no estado global
3. Toda vez que o estado muda os componentes que estao usando aquele reducer sao avisados e atualizados.

## Aula 11 - Reactotron + Redux

Vamos configurar o ***Reactotron*** pois ele vai ajudar bastante a debugar a aplicaçāo com Redux.

1. Rodar `yarn add reactotron-react-js reactotron-redux`
2. Dentro de `src` criamos uma pasta `config` com um arquivo `ReactotronConfig.js`

`ReactotronConfig.js`:

```
import Reactotron from 'reactotron-react-js';
import { reactotronRedux } from 'reactotron-redux';

if (process.env.NODE_ENV === 'development') {
  const tron = Reactotron.configure().use(reactotronRedux()).connect();

  tron.clear();

  console.tron = tron;
}
```

3. Vamos no arquivo `.eslintrc.js` e colocamos dentro de `rules`:

`'no-console': ["error", {allow: ["tron"]}]`

4. Vamos em `src > store > index.js` e colocamos assim:

```
import { createStore } from 'redux';

import rootReducer from './modules/rootReducer';

* const enhancer =
*   process.env.NODE_ENV === 'development' ? console.tron.createEnhancer() : null;

const store = createStore(rootReducer, enhancer);
                                       ********

export default store;
```
5. Vamos em `src > App.js` e acima da importacao de store colocamos:

`import './config/ReactotronConfig';`

### FIM

Agora se clicarmos em ***Adicionar ao carrinho*** ele ira dar um console.log la no Reactotron.

subscription do reactotron: "cart" = retorna os valores que estao dentro do reducer de cart;
snapshots: salvamos o estado e se dermos upload retorna o estado que tava antes.

## Aula 12 - Listando no carrinho

Vamos listar na rota `/cart` todos os produtos que adicionamos no carrinho.

1. Vamos em `src > pages > Cart > index.js` e vamos fazer o seguinte:

```
...
import { connect } from 'react-redux';
...
```
depois tiramos o export default na de cima e passamos para baixo adicionando uma funcao `mapStateToProps` para pegar todos os dados que temos dentro do carrinho:

```
...
const mapStateToProps = (state) => ({
  cart: state.cart,
});

export default connect(mapStateToProps)(Cart);
```

A partir desse momento a a funcao do carrinho ja tem acesso a uma propriedade `cart` -> (`function Cart({ cart }) {`)

2. Vamos em `src > store > cart > reducer.js` e nosso reducer que estava assim:

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
vai ficar assim:

```
export default function cart(state = [], action) {
  switch (action.type) {
    case 'ADD_TO_CART':
      return [
        ...state,
     *   {
          ...action.product,
     *     amount: 1,
     *   },
      ];
    default:
      return state;
  }
}

```

3. Nossa funçāo `Cart` agora vai ficar assim:

```
function Cart({ cart }) {
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
  *        {cart.map((product) => (
            <tr>
              <td>
                <img src={product.image} alt={product.title} />
                          *********************************
              </td>
              <td>
                <strong>{product.title}</strong>
                         *************
                <span>{product.priceFormatted}</span>
                       **********************
              </td>
              <td>
                <div>
                  <button type="button">
                    <MdRemoveCircleOutline size={20} color="#245edb" />
                  </button>
                  <input type="number" readOnly value={product.amount} />
                                                       *************
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
          ))}
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
 Agora so falta juntarmos produtos do mesmo tipo, calcular o total, e permitir que o usuario adicione mais quantidade do produto pelos botoes + e -

## Aula 13 - Produto duplicado

Nessa aula vamos lidar com os produtos duplicados, ou seja, em vez de exibir dois produtos iguais no carrinho vamos apenas listar uma vez e adicionar a quantidade dele no input.

E para isso vamos utilizar uma ferramenta chamada ***Immer***

### Configurando

1. `yarn add immer`
2. Em `src > store > modules > cart > reducer.js` nosso reducer que estava assim:

```
export default function cart(state = [], action) {
  switch (action.type) {
    case 'ADD_TO_CART':
      return [
        ...state,
        {
          ...action.product,
          amount: 1,
        },
      ];
    default:
      return state;
  }
}
```

vai ficar assim:

```
* import produce from 'immer';

export default function cart(state = [], action) {
  switch (action.type) {
    case 'ADD_TO_CART':
*      return produce(state, (draft) => {
*        const productIndex = draft.findIndex((p) => p.id === action.product.id); // Verifica se ja tem um produto com aquele id quele estado
*
*        if (productIndex >= 0) { // SE TIVER SO VAMOS ADICIONAR UM NO AMOUNT
*          draft[productIndex].amount += 1;
*        } else { // SE NAO TIVER VAMOS CRIAR NORMALMENTE
*          draft.push({
*            ...action.product,
*            amount: 1,
*          });
*        }
*      });
    default:
      return state;
  }
}
```
## Aula 14 - Remover produto

Quando clicarmos na lixeira o produto que ele clicar saira do carrinho.

1. Vamos em `src > pages > Cart > index.js` e fazemos o seguinte:

passamos um novo parametro na funçao:

```
...
function Cart({ cart, dispatch }) { ...
                      ********
...
```

2 Vamos no button e criamos a funçāo:

```
<button
  type="button"
*  onClick={() =>
*    dispatch({ type: 'REMOVE_FROM_CART', id: product.id })
*  }
>
```

3. Vamos em `src > store > modules > cart > reducer.js` e no nosso reducer adicionamos o seguinte(*):

```
import produce from 'immer';

export default function cart(state = [], action) {
  switch (action.type) {
    case 'ADD_TO_CART':
      return produce(state, (draft) => {
        const productIndex = draft.findIndex((p) => p.id === action.product.id);

        if (productIndex >= 0) {
          draft[productIndex].amount += 1;
        } else {
          draft.push({
            ...action.product,
            amount: 1,
          });
        }
      });
 *   case 'REMOVE_FROM_CART':
 *     return produce(state, (draft) => {
 *       const productIndex = draft.findIndex((p) => p.id === action.id);
 *
 *       if (productIndex >= 0) {
 *         draft.splice(productIndex, 1);
 *       }
 *     });
    default:
      return state;
  }
}
```
com isso ao clicarmos na lixeira ele excluirá aquele produto.

## Aula 15 - Refatorando Actions

Vamos refatoras as actions para ficar algo mais facil de ler e lidar com eventuais bugs.

1. Dentro de `src > store > modules > cart` criamos um arquivo `actions.js`, vamos no Home e no Cart e copiamos o que esta dentro do `dispatch`.

 Nosso arquivo `actions.js` vai ficar assim:

```
export function addToCart(product) {
  return {
    type: 'ADD_TO_CART',
    product,
  };
}

export function removeFromCart(id) {
  return {
    type: 'REMOVE_FROM_CART',
    id,
  };
}
```

2. ai vamos nos arquivos que usamos essas actions e fazemos o seguinte:

```
...
import * as CartActions from '../../store/modules/cart/actions';
...
```
e colocamos os dispatch's assim:

```
...
dispatch(CartActions.addToCart(product));
...
dispatch(CartActions.removeFromCart(product.id));
...
```

3. podemos facilitar ainda mais fazendo o seguinte:

No arquivo onde temos as actions sendo usadas:

```
...
import { bindActionCreators } from 'redux';
...
```

e la no final acima fazemos o seguinte:

```
...
const mapDispatchToProps = dispatch =>
  bindActionCreators(CartActions, dispatch);

export default connect(null, mapDispatchToProps)(Home);
```

no caso ali passamos `null` pois sera o `mapStateToProps` que nao temos ainda, e fazemos isso nos arquivos que temos as actions sendo usadas.

Fazendo isso, nossas actions que estavam sendo chamadas assim:

`dispatch(CartActions.addToCart(product));`

agora podemos chamar assim:

```
handleAddProduct = (product) => {
    const { addToCart } = this.props;

 *   addToCart(product);
  };
```

***Exemplo 2:*** `src > pages > Cart > index.js`:

```
const mapDispatchToProps = (dispatch) =>
  bindActionCreators(CartActions, dispatch);

export default connect(mapStateToProps, mapDispatchToProps)(Cart);
```

La na `function Cart` passamos como prop a funcao que queremos usar (addToCart ou RemoveFromCart):

`function Cart({ cart, removeFromCart }) { ...`

e no botao:

```
<button
  type="button"
  onClick={() => removeFromCart(product.id)}
>
```
4. outras coisa que podemos fazer agora é renomear a action pois como ela esta separada agora de onde ela é usada fica mais facil lidar com bugs.

Entao para fazer isso vamos primeiro em `src > store > modules > cart > actions.js` e mudamos o nome das actions, ficando assim por exemplo:

```
export function addToCart(product) {
  return {
    type: '@cart/ADD',
           *********
    product,
  };
}

export function removeFromCart(id) {
  return {
    type: '@cart/REMOVE',
           ************
    id,
  };
}
```
depois vamos em `store > modules > cart > reducer.js` e mudamos o nome antigo que ele esta ouvindo para o novo que configuramos;

***EX:*** `case '@cart/ADD':`

## Aula 16 - Alterando quantidade

Vamos fazer as funcionalidades de adicionar mais um no input clicando nos botões de (+) e (-) alterando o valor no input.

1. Vamos no nosso arquivo `store > modules > cart > actions.js` e adicionamos uma nova function:

```
export function updateAmount(id, amount) {
  return {
    type: '@cart/UPDATE_AMOUNT',
    id,
    amount,
  };
}
```

2. Vamos em `pages > Cart > index.js` e acima do return colocamos essa function:

```
function Cart({ cart, removeFromCart, updateAmount }) {
                                      ************
*  function increment(product) {
*    updateAmount(product.id, product.amount + 1);
*  }
*  function decrement(product) {
*    updateAmount(product.id, product.amount - 1);
*  }
```

3. Adicionamos essa functions nos nossos botões:

```
<button type="button" onClick={() => decrement(product)}>
                      *********************************
  <MdRemoveCircleOutline size={20} color="#245edb" />
</button>
<input type="number" readOnly value={product.amount} />
<button type="button" onClick={() => increment(product)}>
                      *********************************
  <MdAddCircleOutline size={20} color="#245edb" />
</button>
```

4. Agora vamos em `store > modules > cart > reducer.js` e adicionamos um novo `case`:

```
case '@cart/UPDATE_AMOUNT': {
      if (action.amount <= 0) {
        return state;
      }

      return produce(state, (draft) => {
        const productIndex = draft.findIndex((p) => p.id === action.id);

        if (productIndex >= 0) {
          draft[productIndex].amount = Number(action.amount);
        }
      });
    }
```

## Aula 17 - Calculando totais

Vamos calcular o Subtotal e o Total da compra.

### Subtotal

1. Vamos em `pages > Cart > index.js` e la no final nosso `mapStateToProps` que estava assim:

```
const mapStateToProps = (state) => ({
  cart: state.cart,
});
```
vai ficar assim:

```
...
import { fromatPrice } from '../../util/format';
...

const mapStateToProps = (state) => ({
  cart: state.cart.map((product) => ({
    ...product,
    subtotal: formatPrice(product.price * product.amount),
  })),
});
```
Mapeamos todo o array de produtos pegando cada produto e copiamos todos os dados nele existente, passando um novo campo `subtotal` que calcula o preco do produto vezes a quantidade que tem dele no carrinho.

2. Agora é so adicionar na tag que queremos ver o subtotal:

`<strong>{product.subtotal}</strong>`

### Total

1. Para isso vamos denovo no `mapStateToProps` que agora vai ficar assim:

```
const mapStateToProps = (state) => ({
  cart: state.cart.map((product) => ({
    ...product,
    subtotal: formatPrice(product.price * product.amount),
  })),
*  total: formatPrice(
*    state.cart.reduce((total, product) => {
*      return total + product.price * product.amount;
*    }, 0)
*  ),
});
```

2. Vamos la em cima na function `cart` e passamos o `total` como parametro na funcao:

```
function Cart({ cart, total, removeFromCart, updateAmount }) {
                      *****
```

3. Vamo na tag que queremos e passamo o valor que vai receber o total:

`<strong>{total}</strong>`

## Aula 18 - Exibindo quantidades

Do lado do adicionar ao carrinho vamos exibir quantos daquele produto ja estao no carrinho.

1. Vamos em `pages > Home > index.js` e la embaixo perto do nosso export default, o que estava assim:

```
const mapDispatchToProps = (dispatch) =>
  bindActionCreators(CartActions, dispatch);

export default connect(null, mapDispatchToProps)(Home);
```

vai ficar assim:

```
* const mapStateToProps = (state) => ({
*   amount: state.cart.reduce((amount, product) => {
*     amount[product.id] = product.amount;
*
*     return amount;
*   }, {}),
* });

const mapDispatchToProps = (dispatch) =>
  bindActionCreators(CartActions, dispatch);

export default connect(mapStateToProps, mapDispatchToProps)(Home);
                       ***************
```
2. Vamos la em cima depois dentro do `render()`:

`const { amount } = this.props;`

3. passamos o valor na tag:

```
<div>
  <MdAddShoppingCart size={16} color="#fff" />{' '}
  {amount[product.id] || 0}
</div>
```
