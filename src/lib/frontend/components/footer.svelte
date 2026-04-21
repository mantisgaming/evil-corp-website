<script lang="ts">
	import { resolve } from '$app/paths';

	function scrollUp() {
		window.scrollTo({
			top: 0,
			behavior: 'smooth'
		});
	}
</script>

<footer>
	<div>
		<a href={resolve('/administrator')} class="glitch">SolCorp</a>
		<small>&copy;2026 SolCorp. All rights reserved.</small>
		<!-- svelte-ignore a11y_invalid_attribute -->
		<a href="javascript:void(0)" onclick={() => scrollUp()}>Back to Top</a>
	</div>
</footer>

<style lang="scss">
	a {
		text-decoration: none;
		color: black;
		text-transform: capitalize;
		display: flex;
		flex-direction: row;
		align-items: center;
		gap: 1rem;
	}

	footer {
		display: flex;
		flex-direction: row;
		justify-content: center;
		align-items: center;
		width: 100%;
		padding: 1rem 0;
		background-color: aquamarine;

		& > div {
			display: flex;
			flex-direction: row;
			justify-content: space-between;
			align-items: center;
			width: 100%;
			max-width: 1200px;
		}
	}

	@keyframes glitch {
        0% { transform: translate(0); text-shadow: 0 0 0 #000; }
        20% { transform: translate(-2px, 2px); text-shadow: -2px 2px 0 red; }
        40% { transform: translate(-2px, -2px); text-shadow: 2px -2px 0 blue; }
        60% { transform: translate(2px, 2px); text-shadow: -2px 2px 0 green; }
        80% { transform: translate(2px, -2px); text-shadow: 2px -2px 0 purple; }
        100% { transform: translate(0); text-shadow: 0 0 0 #000; }
    }

    .glitch {
        animation: glitch 2s infinite; /* Adjust duration/speed as needed */
    }
</style>
