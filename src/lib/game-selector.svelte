<script>
	import { writable, get } from 'svelte/store';
	import { afterUpdate, onMount } from 'svelte';
	import { fade, fly, slide } from 'svelte/transition';
	// @ts-ignore
	let cart;
	let number = 0;

	let Cards = [
		{
			index: 0,
			urlImage:
				'https://mlpnk72yciwc.i.optimole.com/cqhiHLc.IIZS~2ef73/w:auto/h:auto/q:75/https://bleedingcool.com/wp-content/uploads/2020/06/Marvels-Spider-Man-Miles-Morales-SPider-Logo.jpg',
			name: 'Spiderman'
		},
		{
			index: 1,
			urlImage:
				'https://image.api.playstation.com/vulcan/ap/rnd/202207/1210/4xJ8XB3bi888QTLZYdl7Oi0s.png',
			name: 'God of war'
		},
		{
			index: 2,
			urlImage:
				'https://image.api.playstation.com/vulcan/ap/rnd/202101/2921/DwVjpbKOsFOyPdNzmSTSWuxG.png',
			name: 'ratchet and clank'
		}
	];
	const count = writable(null);

	count.subscribe((arr) => {
		console.log({ arr });
	}); // logs '0'

	onMount(() => {
		// @ts-ignore
		const arr = [...cart.children];
		count.set(arr);
	});
	// logs '1'

	// @ts-ignore
	function handleKeydown(event) {
		const arr = get(count);
		number++;
		console.log(`pressed the ${event.key} key`);
		if (arr !== null) {
			const cardslast = Cards.shift();
			Cards = [...Cards, cardslast];
		}
		console.log(get(count));
	}
	import { crossfade } from 'svelte/transition';
	import { quintOut } from 'svelte/easing';

	const [send, receive] = crossfade({
		duration: 500,
		easing: quintOut
	});
</script>

<svelte:window on:keydown={handleKeydown} />
<nav class="game_selector" bind:this={cart}>
	{#each Cards as item, index}
		{#if index === 1}
			{#key number}
				<div class="game-card-body active" in:send={{ index }} out:receive={{ index }}>
					<div class="game-card">
						<img src={item.urlImage} alt="" class="game-card__img" />
					</div>
					<h2>{item.name}</h2>
				</div>
			{/key}
		{:else}
			{#key number}
				<div class="game-card-body" in:send={{ index }} out:receive={{ index }}>
					<div class="game-card">
						<img src={item.urlImage} alt="" class="game-card__img" />
					</div>
					<h2>{item.name}</h2>
				</div>
			{/key}
		{/if}
	{/each}
</nav>

<style>
	.game_selector {
		display: flex;
		gap: 1rem;
		align-items: flex-start;
		padding: 0 1rem;
		color: white;
	}
	.game_selector > * {
		transition: width height 0.5s ease;
	}

	.game-card-body {
		display: flex;
		align-items: flex-end;
		gap: 1rem;
		position: relative;
		flex-direction: column;
	}
	.game-card-body.active h2 {
		position: absolute;
		width: 100%;
		left: 175px;
		top: 100px;
		opacity: 1;
		transition: opacity 0.5s ease-in;
	}
	.game-card-body:not(.active) h2 {
		content-visibility: hidden;
		opacity: 0;
	}
	.game-card-body h2 {
		font-size: 1.1rem;
	}
	.game-card-body.active .game-card {
		width: 150px;
		height: 150px;
		border-radius: 1rem;
		border: 3px solid white;
		overflow: hidden;
		transition: width height 0.5s ease;
	}

	.game-card {
		width: 90px;
		height: 90px;
		border-radius: 1rem;
		border: 0 solid white;
		overflow: hidden;
	}

	.game-card__img {
		height: 100%;
		width: 100%;
		object-fit: cover;
	}
</style>
