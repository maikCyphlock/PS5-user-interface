<script>
	import Navbar from '$lib/navbar.svelte';
	import GameSelector from '$lib/game-selector.svelte';
	import GameList from '$lib/gameList.js';
	let url;
	let parentProperty = '';

	function handleUpdateProperty(event) {
		parentProperty = event.detail.value;
		url = GameList[parentProperty].urlBanner;

		console.log();
	}
</script>

<main class="relative">
	<Navbar />
	<GameSelector on:updateProperty={handleUpdateProperty} />
	<div class="container">
		<img src={url} class="bg" alt="" />
	</div>
</main>

<style>
	.relative {
		position: relative;
		overflow: hidden;
		min-height: 100vh;
		min-width: 100vw;
	}

	.bg {
		filter: brightness(0.6);
		position: absolute;
		height: 100%;
		width: 100%;
		top: 0;
		z-index: -2;

		object-fit: cover;
	}
	:global(body) {
		/* this will apply to <body> */
		font-family: 'Poppins', sans-serif;
		margin: 0;
		padding: 0;
		box-sizing: border-box;
	}
</style>
