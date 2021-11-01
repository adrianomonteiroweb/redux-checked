# Checklist React-Redux

*Antes de começar*
- [x] Definir como o estado global será iniciado
- [x] Definir as actions iniciais para o projeto

*Instalando o react-redux em seu projeto*
- [x] npm install react-redux

*Em o redux comum, use*
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

*No arquivo store/index.js:*
- [x] Importe o rootReducer e crie a store
- [x] Configure o [Redux DevTools](https://github.com/reduxjs/redux-devtools)

*Na pasta reducers:*
- [x] extruture o index.js para ser um rootReducer
### exemplo:
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
- [x] crie os actionTypes. exe: `const ADD_TO_CART = 'ADD_TO_CART';`
- [x] crie os actions creators necessários

*Nos componentes:*
- [x] crie a função mapStateToProps
- [x] crie a função mapDispatchToProps
- [x] faça o connect