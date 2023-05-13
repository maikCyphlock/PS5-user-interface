<script>
	import GlassIcon from './icons/glass-icon.svelte';
	import CogIcon from './icons/cog-icon.svelte';
</script>

<nav>
	<div class="play-area">
		<a href="/"> Games </a>
		<a href="/map/"> Media </a>
	</div>
	<div class="icon">
		<GlassIcon />
		<CogIcon />
		<div class="date">10:50 PM</div>
	</div>
</nav>

<style scoped>
	:global(svg) {
		height: 1.5rem;
		width: 1.5rem;
	}
	/* header elements */
	nav {
		display: flex;
		gap: 1rem;

		justify-content: space-around;
		align-items: center;
		min-height: 50px;
		& div.play-area {
			display: flex;
			gap: 3rem;
			align-items: flex-end;
			font-weight: 700;
			font-size: 1.1rem;
			& a {
				text-decoration: none;
				color: rgb(255, 255, 255);
			}
		}
		& div.icon {
			display: flex;
			gap: 1.5rem;
			color: rgb(255, 255, 255);
		}
	}
	.date {
		color: rgb(255, 255, 255);
	}
</style>
