
# React Style Guide

Minha abordagem sobre arquitetura de projeto para padronizar nosso Frontend. Todos esses conceitos foram baseados em estudos que fiz "pelas internets".

### Nomenclatura

Para uma padronização, utilizaremos PascalCase para componentes e arquivos. Para instâncias usaremos camelCase.

```js
// Não considere
import todoList from './TodoList';

// Considere
import TodoList from './TodoList';

// Não considere
const TodoItem = <TodoList />;

// Considere
const todoItem = <TodoList />;
```

Para chamar componentes, dentro do seu domínio deverá ser criado um arquivo *index* que instância o módulo.

```js
// Não considere
import TodoList from './TodoList/TodoList';

// Não considere
import TodoList from './TodoList/index';

// Considere
import TodoList from './TodoList';
```

### Use regular function para criar os componentes

Tendo como base performance, *less code* e usando *Context Api*, todos os componentes deverão ser escritos no padrão funcional, usando *regular functions*.

```js
// Não considere
class TodoList extends React.Component {
	// ...
	render() {
		return <div>{this.state.hello}</div>;
	}
};

// Considere
function TodoList() = {
	// ...
	return <div>{this.state.hello}</div>;
}
```

***Por que?*** Você não consegue usar "React Hook" em um "extended component";

***Por que?*** Usando *regular function* no lugar de uma *arrow function* você ainda tem o `this` dentro do contexto;

***Por que?*** Os argumentos do tipo objeto não existem dentro de uma *arrow function*;

```js
// OK
const user = {       
	show(){ 
		console.log(arguments); 
	} 
}; 
user.show(1, 2, 3); 

// ReferrenceError
const user = {      
	show_ar : () => { 
		console.log(...arguments); 
	} 
}; 
user.show_ar(1, 2, 3);
```

***Por que?*** As *regular functions* criadas usando declarações ou expressões de função são "construtivas" e "chamáveis";

```js
// OK
let x = function(){ 
	console.log(arguments); 
}; 
new x =(1,2,3); 

// TypeError
let x = ()=> { 
	console.log(arguments); 
}; 
new x(1,2,3);
```
