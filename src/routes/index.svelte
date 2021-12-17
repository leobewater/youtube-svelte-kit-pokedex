<script context="module">
	// SSR (server side rendering)
	// run this query before showing the page
	export async function load({ page }) {
		const url = `https://pokeapi.co/api/v2/pokemon?limit=150`;
		const res = await fetch(url);
		const data = await res.json();

		// add id and image to each result
		const loadedPokemon = data.results.map((data, index) => {
			return {
				name: data.name,
				id: index + 1,
				image: `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${
					index + 1
				}.png`
			};
		});

		return { props: { pokemon: loadedPokemon } };
	}
</script>

<script>
	//import { pokemon } from '../stores/pokestore.js';
	import PokemanCard from '../components/pokemanCard.svelte';

	export let pokemon;

	// console.log($pokemon); // add "$" make it reactive

	let searchTerm = '';
	let filteredPokemon = [];

	// make reactive
	$: {
		console.log(searchTerm);
		if (searchTerm) {
			// search and filter the pokemon
			filteredPokemon = pokemon.filter((pokeman) =>
				pokeman.name.toLowerCase().includes(searchTerm.toLowerCase())
			);
		} else {
			// reset the filter and show all pokemons
			filteredPokemon = [...pokemon];
		}
	}
</script>

<svelte:head>
	<title>Svelte Kit Pokedex</title>
</svelte:head>

<h1 class="text-4xl text-center my-8 uppercase">Svelte Kit Pokedex</h1>

<input
	class="w-full rounded-md text-lg p-4 border-2 border-gray-200"
	type="text"
	bind:value={searchTerm}
	placeholder="Search Pokemon"
/>

<div class="py-4 grid gap-4 md:grid-cols-2 grid-cols-1">
	{#each filteredPokemon as pokeman}
		<PokemanCard {pokeman} />
	{/each}
</div>
