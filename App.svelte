<script>
	import PokedexEntry from "./PokedexEntry.svelte";

	let pokemons = [];
	let filterKeyword = "";
	$: filteredPokemons = pokemons.filter((pokemon) => pokemon.name.startsWith(filterKeyword) 
		|| pokemon.primaryType.startsWith(filterKeyword));

	async function fetchPokemons(){
		let query = await fetch("https://pokeapi.co/api/v2/pokemon?limit=600");
		if(!query.ok){
			throw new Error("Failed to load pokemons");
		}

		let queryData = await query.json();

		for(const result of queryData.results){
			let pokemonQuery = await fetch(result.url);
			if(pokemonQuery.ok){
				let pokemonData = await pokemonQuery.json();
				let pokemon = { 
					"name": pokemonData.name, 
					"primaryType": pokemonData.types[0].type.name, 
					"imageUrl": pokemonData.sprites.other["official-artwork"].front_default
				};
				if(pokemonData.types[1]){
					pokemon.secondaryType = pokemonData.types[1].type.name;
				}
				pokemons.push(pokemon);
				pokemons = pokemons;
			}
		}
	}

	fetchPokemons();
</script>

<main>
	<h1>Pokedex</h1>
	<input placeholder="Filter by name or type" bind:value={filterKeyword}/>
	<br/>
	{#each filteredPokemons as pokemon}
		<PokedexEntry {...pokemon}/>
	{/each}
</main>

<style>
	input {
		min-width: 400px;
	}

	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>