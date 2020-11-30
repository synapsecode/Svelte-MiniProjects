<script>
export let data;
export let onEditTodo;
export let onDeleteTodo;
export let onCompleteTodo;

let isEditing = false;

let t = '', s = '';

const eTodo = () => {
	isEditing = !isEditing;
	onEditTodo(data.id, t, s);
}
</script>

<div class="td {data.completed ? ' cmp' : ''}">
	<div class="c1">
		<div class="compcheck" on:click={onCompleteTodo(data.id)}>
			{#if data.completed}
				<div class="tck">
					✔️
				</div>
			{/if}
		</div>
	</div>
	<div class="c2">
		{#if isEditing}
			<input type="text" bind:value={t} placeholder="title">
			<input type="sp text" bind:value={s} placeholder="subtitle">
		{:else}
			<h3>{data.title}</h3>
			<p class="sp">{data.subtitle}</p>
		{/if}
		
	</div>
	<div class="c3">
		<button on:click={onDeleteTodo(data.id)}>
			🗑️
		</button>
		<button on:click={eTodo} class="{isEditing ? 'e' : 'o'}">
			✍️
		</button>
	</div>
</div>

<style>
.tck{
	margin-top: 2px;
	cursor: pointer;
}
.e{
	border: 2px solid orangered;
}
.td{
	border: 1px solid gray;
	margin: 5px;
	padding: 5px;
	display: flex;
	text-align:center;
}
.c1{
	flex:1;
	margin:auto;
}
.c2{
	flex:3;
	margin:auto;
	text-align: left;
}
.c3{
	flex:2;
	margin:auto;
}
.compcheck{
	border-radius: 500px;
	border:1px solid black;
	background-color: white;
	height: 25px;
	width: 25px;
	margin-left: 20px;
}
.cmp{
	background-color: orangered;
	color: white;
}
.sp{
	margin-top: -18px;
}
</style>