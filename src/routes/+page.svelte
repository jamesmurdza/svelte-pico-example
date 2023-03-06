<script>
	import { onMount } from 'svelte';

	async function callAPI(URL) {
		// Call the API, wait for response, and parse response.
		let response = await fetch(URL, settings);
		let responseData = await response.json();
		return responseData.response;
	}

	// Authorization needed to connect to the API.
	const settings = {
		"headers": {
			"X-RapidAPI-Key": "API_KEY",
			"X-RapidAPI-Host": "api-football-v1.p.rapidapi.com"
		}
	};

	// These variables are the page state.
	let leagues = [];

	// This function is called once to load the page.
	async function loadData() {
		leagues = await callAPI("https://api-football-v1.p.rapidapi.com/v3/leagues?current=true")
	}
	onMount(loadData);
</script>

<h1>Leagues:</h1>
<ul>
	{#each leagues as league}
		<li>{league.league.name}</li>
	{/each}
</ul>