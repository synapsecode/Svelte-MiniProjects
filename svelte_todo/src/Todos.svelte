<script>
import Todo from './Todo.svelte';
const getDataFromFirebase = () => {
	console.log("Got Data from Firebase");
	let x = [
		{
			'id': 1,
			'completed': false,
			'timestamp': Date.now() + 10,
			'title': 'Learn Svelte',
			'subtitle': 'Learn Everything that is a part of svelte 3',
		},
		{
			'id': 2,
			'completed': false,
			'timestamp': Date.now() + 20,
			'title': 'Learn React Native',
			'subtitle': 'Learn React Native!',
		},
		{
			'id': 3,
			'completed': false,
			'timestamp': Date.now() + 30,
			'title': 'Master Flutter',
			'subtitle': 'Gain Complete Mastery over Flutter',
		},
	];
	return {
		'length': x.length,
		'todos':x,
	}
};

let cTitle, cSubtitle;

let todos = getDataFromFirebase()['todos'];

const addTodo = () => {
	let todo = {
		'id': todos[todos.length - 1]['id']+1,
		'completed': false,
		'timestamp': Date.now(),
		'title': cTitle,
		'subtitle': cSubtitle,
	};
	//Add to Firebase
	cTitle = '';
	cSubtitle = '';
	todos = [...todos, todo];
}

const deleteTodo = (id) => {
	console.log("Delete Todo Called");
	let index = -1;
	for(let i in todos){
		console.log(i);
		if(todos[i]['id'] === id){
			index = i;
			break;
		}
	}
	index === -1 ? console.log("Cannot Delete Todo") : todos.splice(index, 1);
	todos = todos;
	//Delete From Firebase
};

const editTodo = (id, t, s) => {
	console.log("Edit Todo Called");
	for(let i of todos){
		if(i['id'] === id){
			i['title'] = t;
			i['subtitle'] = s;
			break;
		}
	}
	todos = todos;
}

const toggleComplete = (id) => {
	console.log("Toggle Complete Called");
	for(let i of todos){
		if(i['id'] === id){
			i['completed'] = !i['completed'];
			console.log("c: " + i);
			break;
		}
	}
	todos = todos;
}

$: {
	console.log(todos);
}



</script>

<div class="xt">
<form on:submit|preventDefault="">
	<input type="text" placeholder="Title" bind:value={cTitle}> 
	<input type="text" placeholder="Subtitle" bind:value={cSubtitle}>
	<button on:click={addTodo} class="ad">
		Add
	</button>
</form>
</div>
<div class="todos">
	{#if todos.length == 0}
		<br>
		<p class="nt">[ No Todos ]</p>
	{/if}
	{#each todos as todo}
		<Todo onEditTodo={editTodo} onCompleteTodo={toggleComplete} onDeleteTodo={deleteTodo} data={todo}/>
	{/each}
</div>

<style>
.todos{
	width: 460px;
	border: 1px solid orangered;
	padding: 5px;
	height: 420px;
	overflow-y: scroll;
}
.ad{
	padding: 5px 10px;
	width: 100px;
	height: 35px;
	color: white;
	background-color: orangered;
}

.nt{
	color: rgba(0, 0, 0, 0.534);
}
</style>