<script>
    import {pokemon} from "../stores/pokestore.js";
    // console.log($pokemon); // add "$" make it reactive
</script>

<svelte:head>
    <title>Svelte Kit Pokedex</title>
</svelte:head>

<h1>Svelte Kit Pokedex</h1>

{#each $pokemon as pokeman}
<p>{pokeman.name}</p>
{/each}


<style>
	h1 {
		color: rgb(89, 210, 49);
	}
</style>
