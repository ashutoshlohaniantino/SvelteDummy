<script>
	import { onMount } from 'svelte';
	import { writable } from 'svelte/store';
  
	// Created a writable store to hold the data
	const data = writable([]);
	console.log(data);
  
	async function fetchData() {
	  try {
		const response = await fetch('https://dummyjson.com/products');
		const jsonData = await response.json();
		console.log(jsonData);
		// Update the store with the fetched data
		data.set(jsonData.products); 
	  } catch (error) {
		console.error('Error fetching data:', error);
	  }
	}
  
	// Trigger the API call when the component is mounted
	onMount(fetchData);
  </script>
  
  <main>
	{#if $data.length > 0} 
	  <ul>
		{#each $data as item (item.id)} 
		  <li>{item.brand} - {item.category} - ${item.price}</li>
		{/each}
	  </ul>
	{:else}
	  <p>Loading data...</p>
	{/if}
  </main>
  
  <style>
	ul {
	  list-style: none;
	  padding: 0;
	}
  
	li {
	  margin-bottom: 0.5rem;
	}
  </style>
  
  <!-- <script>
	import Nested from './Nested.svelte';
    let name = 'Rick Astley';
</script>

<style>
	h1 {
		color: purple;
		font-family: 'Comic Sans MS', cursive;
		font-size: 5em;
	}
</style>

<h1>Hello {name}!</h1>
<Nested/>
<iframe title="dance" src="https://giphy.com/embed/g7GKcSzwQfugw" width="480" height="407" frameBorder="0" class="giphy-embed" allowFullScreen></iframe><p></p>
<p>Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation</p> -->