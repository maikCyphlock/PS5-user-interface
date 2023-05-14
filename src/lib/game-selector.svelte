<script>
	import GameList from './GameList';
	import { register } from 'swiper/element/bundle';
	import { createEventDispatcher } from 'svelte';
	// register Swiper custom elements
	let swiper;
	let number = 0;
	const dispatch = createEventDispatcher();

	const onProgress = (e) => {
		const [swiper, progress] = e.detail;
		console.log(swiper.activeIndex);
		dispatch('updateProperty', { value: swiper.activeIndex });
	};
	const activeIndexChange = (e) => {
		number++;
	};
	register();
</script>

<nav class="game_selector">
	<swiper-container
		slides-per-view={6}
		centered-slides={true}
		keyboard={true}
		cssMode={true}
		on:progress={onProgress}
		on:swiper={(e) => (swiper = e.detail[0])}
	>
		{#each GameList as item}
			<swiper-slide>
				<div class="game-card-body">
					<div class="game-card">
						{#if item.urlImage}
							<img src={item.urlImage} alt="" class="game-card__img" />
						{/if}
					</div>
					<h2 class="text">{item.name}</h2>
				</div>
			</swiper-slide>
		{/each}
	</swiper-container>
</nav>

<style>
	swiper-container {
		height: 80vh !important;
	}
	.game_selector {
		display: flex;
		gap: 1rem;
		align-items: flex-start;
		padding: 0 1rem;
		color: white;
	}
	.game-card-body {
	}
	.swiper-slide-active .game-card-body .text {
		position: fixed;
		width: 100%;
		height: 100%;
		left: 195px;
		top: 100px;
		opacity: 1;
		transition: opacity 0.5s ease-in;
	}
	:not(.swiper-slide-active) .game-card-body h2 {
		opacity: 0;
	}
	.game-card-body h2 {
		font-size: 2rem;
	}
	.swiper-slide-active .game-card-body .game-card {
		width: 150px;
		height: 150px;
		border-radius: 1rem;
		border: 3px solid white;
		overflow: hidden;
	}

	.game-card {
		width: 90px;
		height: 90px;
		border-radius: 1rem;
		border: 0 solid white;
		overflow: hidden;
		transition: all 0.2s ease-in-out;
	}

	.game-card__img {
		height: 100%;
		width: 100%;
		object-fit: cover;
	}
</style>
