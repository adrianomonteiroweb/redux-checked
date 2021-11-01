# Checklist React-Redux

*Antes de começar*
- [ ] Definir como o estado global será iniciado
- [ ] Definir as actions iniciais para o projeto

- [ ] *Instalando o react-redux em seu projeto*
- Use o comando:
```npm
 npm install react-redux
```

- [ ] *Organizando as pastas em "src". Use o terminal se preferir, como a seguir:*
- Use o comando abaixo para criar a pasta "redux" dentro de "src", se preferir.
```
 mkdir src/redux
```
- Use o comando abaixo para criar a pasta "actions" dentro de "src/redux", se preferir.
```
 mkdir src/redux/actions
```
- Use o comando abaixo para criar a pasta "reducers" dentro de "src/redux", se preferir.
```
 mkdir src/redux/reducers
```
- Use o comando abaixo para criar a pasta "store" dentro de "src/redux", se preferir.
```
 mkdir src/redux/store
```

 - [ ] *Na pasta redux/actions, crie o arquivo index.js*
- Use o comando abaixo, se preferir.
```
 touch src/redux/actions/index.js
```

- [ ] *Na pasta redux/reducers, crie o arquivo index.js, além dos reducers iniciais que precisar*
- Use o comando abaixo, se preferir.
```
 touch src/redux/reducers/index.js
```
- Use o comando abaixo, se preferir.
```
 touch src/redux/reducers/outroReducer.js
```

- [ ] *Na pasta redux/store, crie o arquivo index.js*
- Use o comando abaixo, se preferir.
```
 touch src/redux/store/index.js
```

*No arquivo App.js ou Index.js*
- [ ] Defina o Provider, `<Provider store={ store }>`, para fornecer os estados à todos os componentes encapsulados em `<App />`.

### Exemplo no index: import o Provider do 'react-redux' e store do caminho "redux/store/index"
```js
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import { Provider } from 'react-redux';
import store from './redux/store/index';
import App from './App';

ReactDOM.render(
  <Provider store={ store }>
      <App />
  </Provider>,
  document.getElementById('root'),
);
```

*No arquivo redux/store/index.js:*
- [ ] Importe o rootReducer e crie a store.
- [ ] instale o redux-devtoolsextension - mais informações: [Redux DevTools](https://github.com/reduxjs/redux-devtools).
- Use o comando abaixo, se preferir
```
 npm install --save redux-devtools-extension
```
*obs: Utilize a extensão chrome redux-devtools para verificar o estado na aplicação rodando.*

### Exemplo:
```js
import { createStore, applyMiddleware } from 'redux';
import thunk from 'redux-thunk';
import { composeWithDevTools } from 'redux-devtools-extension';
import rootReducer from '../redux/reducers';

const store = createStore(rootReducer, composeWithDevTools(applyMiddleware(thunk)));

export default store;
```

*Na pasta redux/reducers:*
- [ ] estruture o index.js para ser um rootReducer e combinar reducers criados.
### Exemplo de uso do combineReducers:
```js
import { combineReducers } from 'redux'; // importe o combineReducers para unificar quantos reducers precisar
import reducer1 from './reducer1';
import reducer2 from './reducer2';

const rootReducer = combineReducers({ // combinando dois reducers importados do mesmo diretório
  reducer1,
  reducer2,
});

export default rootReducer;
```

### Exemplo de reducer:
```js
import { SET_LOGIN } from '../actions'; // importa a action

const INITIAL_STATE = { // inicia um estado
  email: '',
};

const reducer = (state = INITIAL_STATE, action) => {
  switch (action.type) {
  case SET_LOGIN:
    return { ...state, email: action.payload };
  default:
    return state;
  }
};

export default reducer;
```

*Na pasta redux/actions:*
- [ ] Crie os actionTypes.
- [ ] Crie os actions creators necessários.

### Exemplo de uma action:
```js
export const SET_LOGIN = 'SET_LOGIN';

export const setLogin = (payload) => ({
  type: SET_LOGIN, payload,
});
```

*Nos seus componentes:*
- [ ] Crie a função mapStateToProps.
- [ ] Crie a função mapDispatchToProps.
- [ ] Utilize o connect.

### Exemplo de connect, mapDispachToProps e mapStateToProps: import connect de "react-redux" e é necesário a importação da action setLogin criada anteriormente
```js
const mapDispatchToProps = (dispatch) => ({
  dispatchSetValue: (email) => dispatch(setLogin(email)),
});

const mapStateToProps = (state) => ({ email: state.user.email });

export default connect(mapStateToProps, mapDispatchToProps)(MyComponent);
```

*Este Checklist foi baseado em outro de uma das turmas da Trybe. Faça bom uso!*