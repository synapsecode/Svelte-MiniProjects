<script>
	import Todos from './Todos.svelte';
</script>

<main>
	<h1>Svelte Todo</h1>
	<p class="st">[ Made by Manas Hejmadi ]</p>
	<center>
		<Todos/>
	</center>
</main>

<style>
	main {
		text-align: center;
		max-width: 240px;
		margin: 0 auto;
	}

	

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4rem;
		font-weight: 100;
	}

	.st{
		margin-top: -40px;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>