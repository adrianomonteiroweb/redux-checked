# Checklist React-Redux

*Antes de começar:*
- [ ] Planejar como o estado global será iniciado.
Ex:
```js
 {
   email: '',
 }
```
- [ ] Definir as actions iniciais para o projeto.
- EX: Atualizar email: updateEmail.

- [ ] *Instalando o react-redux em seu projeto.*
- Use o comando:
```
 npm install react-redux
```

*Lembrete: Para colar o comando no terminal use: Ctrl + Shift + V*

- [ ] *Organizando as pastas em "src". A ideia é ter em "src" a pasta redux, e dentro dela as pastas actions, reducers e store.*
- Use o comando abaixo para criar a pasta "redux" dentro de "src", se preferir.
```
 mkdir src/redux && mkdir src/redux/actions && mkdir src/redux/reducers && mkdir src/redux/store
```

 - [ ] *Nas pastas actions, reducers e store, em redux, crie para cada um arquivo index.js.*
- Use o comando abaixo, se preferir.
```
 touch src/redux/actions/index.js && touch src/redux/reducers/index.js && touch src/redux/store/index.js
```

*No arquivo redux/store/index.js:*
- [ ] Importe o rootReducer e crie a store.
- [ ] instale o redux-devtoolsextension. - Mais informações em: [Redux DevTools](https://github.com/reduxjs/redux-devtools).
- Use o comando abaixo, se preferir
```
 npm install --save redux-devtools-extension
```
*obs: Utilize a extensão chrome redux-devtools para verificar o estado na aplicação rodando.*

### Exemplo:
```js
import { createStore, applyMiddleware } from 'redux'; // import além de 'createStore', para criar sua store, a 'applyMiddleware' de 'redux' para que sua aplicação consiga trabalhar actions de forma assíncrona.
import thunk from 'redux-thunk'; // importando também thunk de 'redux-thunk', ativando dentro da 'applyMiddleWare' no seu 'composeWithDevTools'.
import { composeWithDevTools } from 'redux-devtools-extension'; // junto a extensão em seu chrome, poderá trabalhar e monitorar suas actions e estado em tempo real.
import rootReducer from '../redux/reducers/index'; // você importará rootReducer de 'redux/reducers' quando tiver criado. Ele combinará em 1 reducer principal todos os seus reducers necessários. 

const store = createStore(rootReducer, composeWithDevTools(applyMiddleware(thunk)));

export default store;
```

- [ ] *Instale o redux-thunk.*

```
  npm i redux-thunk
```

*No arquivo App.js ou Index.js:*
- [ ] Defina o Provider, `<Provider store={ store }>`, para fornecer os estados à todos os componentes encapsulados em `<App />`.

### Exemplo no index: import o Provider do 'react-redux' e store do caminho "redux/store/index:"
```js
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import { Provider } from 'react-redux'; // import o Provider de 'react-redux'.
import store from './redux/store/index'; // import o store criado em '/redux/store/index'.
import App from './App';
// abaixo, englobe o 'App' em seu 'Provider' passando o parâmetro store. Disponibilizando assim um estado de forma global para sua aplicação.
ReactDOM.render( 
  <Provider store={ store }>
      <App /> 
  </Provider>,
  document.getElementById('root'),
);
```

*Na pasta redux/actions:*
- [ ] Crie os actionTypes.
- [ ] Crie os actions creators necessários.

### Exemplo de uma action:
```js
export const SET_LOGIN = 'SET_LOGIN'; // Define o type da action.

export const setLogin = (payload) => ({ // Recebe em payload o novo objecto vindo via parâmetro da execução da action 'setLogin' em algum ponto da aplicação.
  type: SET_LOGIN, payload,
});
```

*Na pasta redux/reducers:*
- [ ] Crie primeiro seus arquivos reducers, como os de exemplo reducer1.js e reducer2.js para depois importá-los para o index.js. Estruture o index.js para ser um rootReducer e combinar reducers criados.

### Exemplo de reducer, como um reducer1.js. Nesse exemplo teremos 2 (reducer1 e reducer2).
```js
import { SET_LOGIN } from '../actions'; // importa a action

const INITIAL_STATE = { // inicia um estado
  email: '',
};

const reducer1 = (state = INITIAL_STATE, action) => {
  switch (action.type) {
  case SET_LOGIN:
    return { ...state, email: action.payload }; // seta o email quando a action setLogin for acionada em alguma página ou componente da aplicação.
  default:
    return state; // caso a action.type não for a 'SET_LOGIN', ela mantém o estado sem alteração retornando o próprio 'state'.
  }
};

export default reducer1;
```

### Exemplo de uso do combineReducers:
```js
import { combineReducers } from 'redux'; // importe o combineReducers para unificar quantos reducers precisar
// import , quando criados, os reducers necessários para combiná-los aqui.
import reducer1 from './reducer1';
import reducer2 from './reducer2';

const rootReducer = combineReducers({ // combinando dois reducers importados do mesmo diretório
  reducer1,
  reducer2,
});

export default rootReducer;
```

*Nos seus componentes:*
- [ ] Crie a função mapStateToProps.
- [ ] Crie a função mapDispatchToProps.
- [ ] Utilize o connect.

### Agora sim, você pode começar a ler e rescrever seu estado inicial criado em suas pages e components usando o Connect.
*Exemplo de connect, mapDispachToProps e mapStateToProps: import connect de "react-redux", necesária também a importação da action setLogin criada anteriormente em actions!*
```js
const mapDispatchToProps = (dispatch) => ({ // Cria a chave 'dispatchSetValue', que é uma arrow function, para o contexto de estado da página ou componente. A action 'setLogin' criada anteriormente, responsável por reescrever o estado inicial 'email'.
  dispatchSetValue: (email) => dispatch(setLogin(email)),
});

const mapStateToProps = (state) => ({ email: state.reducer1.email }); // Trás para o contexto de estado da página ou componente o estado inicial criado anteriormente. na chave 'email:', armazenando o estado 'state.reducer1.email'.

export default connect(mapStateToProps, mapDispatchToProps)(MyComponent); // usamos o connect para conectar ao banco de dados nossa página ou componente. obs: caso você só precise ler, utilize apenas 'connect(mapStateToProps)(MyComponent)', caso precise apenas reescrever, use o null, para evitar erros em sua aplicação: 'connect(null, mapDispatchToProps)(MyComponent)'.
```

*Este Checklist foi baseado em outro de uma das turmas da Trybe. Faça bom uso!*

<div>
  <table>
    <thead>
      <tr>
        <th>Autor</th>
        <th colspan="2">Contribuições</th>
      </tr>
    </thhead>
    <tbody>
      <tr>
        <td><img src="https://avatars.githubusercontent.com/u/47261292?v=4" alt="Adriano Monteiro" width="100x" /></td>
        <td><img src="https://avatars.githubusercontent.com/u/83843144?v=4" alt="Marcelo Pantoja" width="100x" /></td>
        <td><img src="https://avatars.githubusercontent.com/u/66140620?v=4" alt="Ivan" width="100x" /></td>
      </tr>
      <tr>
        <td style="text-align: center">
          <a href="https://www.linkedin.com/in/adrianomonteiroweb/" target="_blank">Adriano Monteiro</a>
        </td>
        <td style="text-align: center">
          <a href="https://www.linkedin.com/in/marcelo-pantoja-a71a97112/" target="_blank">Marcelo Pantoja</a>
        </td>
        <td style="text-align: center">
          <a href="https://www.linkedin.com/in/ivan-silva-4ba014221/" target="_blank">Ivan</a>
        </td>
      </tr>
      <tr>
        <td style="text-align: center">
          <a href="https://www.linkedin.com/in/adrianomonteiroweb/" target="_blank">LinkedIn</a>
        </td>
        <td style="text-align: center">
          <a href="https://github.com/Pantoja42" target="_blank">GitHub</a>
        </td>
        <td style="text-align: center">
          <a href="https://github.com/Ivandosss" target="_blank">GitHub</a>
        </td>
      </tr>
    </tbody>
  </table>
</div>
