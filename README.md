# Checklist React-Redux

*Antes de começar*
- [ ] Definir como o estado global será iniciado.
- [ ] Definir as actions iniciais para o projeto.

- [ ] *Instalando o react-redux em seu projeto*
- Use o comando:
```
 npm install react-redux
```

- [ ] *Organizando as pastas em "src". A ideia é ter em "src" a pasta redux, e dentro dela as pastas actions, reducers e store.*
- Use o comando abaixo para criar a pasta "redux" dentro de "src", se preferir.
```
 mkdir src/redux && mkdir src/redux/actions && mkdir src/redux/reducers && mkdir src/redux/store
```

 - [ ] *Na pastas actions, reducers e store, em redux, crie para cada um arquivo index.js*
- Use o comando abaixo, se preferir.
```
 touch src/redux/actions/index.js && touch src/redux/reducers/index.js && touch src/redux/store/index.js
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

- [ ] *Instale o redux-thunk*

```
  npm i redux-thunk
```

*Na pasta redux/reducers:*
- [ ] Estruture o index.js para ser um rootReducer e combinar reducers criados. Crie primeiro seus arquivos reducers, como os de exemplo reducer1.js e reducer2.js para depois importá-los para o index.js.
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

### Exemplo de reducer, como um reducer1.js:
```js
import { SET_LOGIN } from '../actions'; // importa a action

const INITIAL_STATE = { // inicia um estado
  email: '',
};

const reducer1 = (state = INITIAL_STATE, action) => {
  switch (action.type) {
  case SET_LOGIN:
    return { ...state, email: action.payload }; // seta o email quando a action setLogin for acionada.
  default:
    return state;
  }
};

export default reducer1;
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

const mapStateToProps = (state) => ({ email: state.reducer1.email });

export default connect(mapStateToProps, mapDispatchToProps)(MyComponent);
```

*Este Checklist foi baseado em outro de uma das turmas da Trybe. Faça bom uso!*

|           Autor           |          Contribuições           |
|:-------------------------:|:--------------------------------:|
|      Adriano Monteiro     |       Ivan      Marcelo Pantoja  |
