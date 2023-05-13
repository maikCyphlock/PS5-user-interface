<script>
	import Navbar from '$lib/navbar.svelte';
	import GameSelector from '$lib/game-selector.svelte';
</script>

<main class="relative">
	<Navbar />
	<GameSelector />
	<img
		src="https://image.api.playstation.com/vulcan/img/rnd/202010/2417/tnCutdREPv6Pa7atqb8MTxGW.png"
		class="bg"
		alt=""
	/>
</main>

<style>
	.relative {
		position: relative;
		overflow: hidden;
		min-height: 100vh;
		min-width: 100vw;
	}
	.bg {
		position: absolute;
		height: 100%;
		width: 100%;
		top: 0;
		z-index: -1;
		filter: brightness(0.8);
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
