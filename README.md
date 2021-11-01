# Checklist React-Redux

*Antes de começar*
- [x] Definir como o estado global será iniciado
- [x] Definir as actions iniciais para o projeto

*Instalando o react-redux em seu projeto*
- [x] npm install react-redux

*ou*
- [x] npm install @reduxjs/toolkit

*Organizando as pastas em "src". Use o terminal se preferir, como a seguir:*
- [x] Use o comando: "mkdir src/redux" para criar a pasta "redux" dentro de "src"
- [x] Use o comando: "mkdir src/redux/actions" para criar a pasta "actions" dentro de "src/redux"
- [x] Use o comando: "mkdir src/redux/reducers" para criar a pasta "reducers" dentro de "src/redux"
- [x] Use o comando: "mkdir src/redux/store" para criar a pasta "store" dentro de "src/redux"

*Na pasta actions, crie o arquivo index.js*
- [x] Use o comando:  "touch src/redux/actions/index.js", se preferir

*Na pasta reducers, crie o arquivo index.js, além dos reducers iniciais que precisar*
- [x] Use o comando:  "touch src/redux/reducers/index.js", se preferir
- [x] Use o comando:  "touch src/redux/reducers/outroReducer.js", se preferir

*Na pasta store, crie o arquivo index.js*
- [x] Use o comando:  "touch src/redux/store/index.js", se preferir

*No arquivo App.js ou Index.js*
- [x] Defina o Provider, `<Provider store={ store }>`, para fornecer os estados à todos os componentes encapsulados em `<App />`.

### Exemplo no index: Provider vem do 'react-redux' e store do caminho "redux/store/index"
```import React from 'react';
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
- [x] Importe o rootReducer e crie a store
- [x] instale o redux-devtoolsextension: "npm install --save redux-devtools-extension" - mais informações: [Redux DevTools](https://github.com/reduxjs/redux-devtools)

### Exemplo:
```import { createStore, applyMiddleware } from 'redux';
import thunk from 'redux-thunk';
import { composeWithDevTools } from 'redux-devtools-extension';
import rootReducer from '../redux/reducers';

const store = createStore(rootReducer, composeWithDevTools(applyMiddleware(thunk)));

export default store;
```

*Na pasta reducers:*
- [x] extruture o index.js para ser um rootReducer e combinar reducers criados
### Exemplo:
```import { combineReducers } from 'redux'; // importe o combineReducers para unificar quantos reducers precisar
import reducer1 from './reducer1';
import reducer2 from './reducer2';

const rootReducer = combineReducers({ // combinando dois reducers importados do mesmo diretório
  reducer1,
  reducer2,
});

export default rootReducer;
```

*Na pasta actions:*
- [x] crie os actionTypes
- [x] crie os actions creators necessários

### Exemplo de uma action:
```export const SET_LOGIN = 'SET_LOGIN';

export const setLogin = (payload) => ({
  type: SET_LOGIN, payload,
});
```

*Nos componentes:*
- [x] crie a função mapStateToProps
- [x] crie a função mapDispatchToProps
- [x] faça o connect

### Exemplo de connect, mapDispachToProps e mapStateToProps: import connect de "react-redux" e é necesário a importação da action setLogin criada anteriormente
```const mapDispatchToProps = (dispatch) => ({
  dispatchSetValue: (email) => dispatch(setLogin(email)),
});

const mapStateToProps = (state) => ({ email: state.user.email });

export default connect(mapStateToProps, mapDispatchToProps)(Login);
```