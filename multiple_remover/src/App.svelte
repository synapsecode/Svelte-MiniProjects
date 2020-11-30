<script>
	let N = 3000;
	let nuked_nums = [];
	let remaining_nums = N;

	const nuke = (n) => {
		console.log("Nuke: " + n);
		if(nuked_nums.includes(n))
			nuked_nums = nuked_nums.filter((v, i, arr) => {return v != n});
		else
			nuked_nums = [...nuked_nums, n];
		blocks = getBlocks();
	}

	const _isNuked = (n) => {
		for(let x of nuked_nums){
			if(n % x == 0)
				return true;
		}
		return false;
	}

	const getBlocks = () => {
		let blocs = [];
		let rn = 0;
		for(let i=0; i<N; i++){
			blocs.push({
				'number': i+1,
				'isNuked': _isNuked(i+1),
				'isEpicenter': nuked_nums.includes(i+1),
			});

			if(_isNuked(i+1))
				rn += 1;
		}
		// console.log(blocs)
		remaining_nums = N - rn;
		return blocs
	}

	let blocks = getBlocks();


	$:{
		console.log("Changed N to: " + N);
		blocks = getBlocks();
	}
</script>

<center
><h1>
	Multiple Nuker <input type="text" bind:value={N}>

</h1>
<center>
	<h1>( Remaining: {remaining_nums} )</h1>
</center>
</center>
<div class="holder">
	<div class="panel">
		{#each blocks as block}
			<div class="bloc{block.isEpicenter ? ' nuked' : block.isNuked ? ' affected' : ' x'}" on:click={() => nuke(block.number)}>
				<center>
					<h1>{block.number}</h1>
				</center>
			</div>
		{/each}
	</div>
</div>




<style>
	.bloc{
		background-color: rgba(255, 255, 255, 0.8);
		border: 1px solid rgba(0, 0, 0, 0.8);
		width: 90px;
		height: 100px;
		margin: 5px;
	}

	.panel{
		height: 500px;
		display: flex;
  		flex-direction: row;
		flex-wrap: wrap;
		margin: 20px 20px -20px 20px;
		overflow-x: scroll;
		border: 1px solid black;
	}
	
	.affected{
		background-color: black;
	}
	
	.nuked{
		background-color: orangered;
	}

	.pr{
		border: 2px solid green;
	}
</style>