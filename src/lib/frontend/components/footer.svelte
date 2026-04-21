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
		padding: 1rem 3rem;
		background-color: aquamarine;

		& > div {
			display: flex;
			flex-direction: row;
			justify-content: space-between;
			align-items: center;
			width: 100%;
			max-width: 1200px;
			gap: 0.5rem;

			@media screen and (width < 500px) {
				flex-direction: column;
			}
		}
	}

	@keyframes glitch {
		5% {
			transform: translate(0);
			text-shadow: 0 0 0 #000;
		}
		10% {
			transform: translate(-3px, 1px);
			text-shadow: -3px 1px 0 red;
		}
		15% {
			transform: translate(0);
			text-shadow: 0 0 0 #000;
		}
		35% {
			transform: translate(0);
			text-shadow: 0 0 0 #000;
		}
		40% {
			transform: translate(-3px, -1px);
			text-shadow: 3px -1px 0 blue;
		}
		45% {
			transform: translate(0);
			text-shadow: 0 0 0 #000;
		}
		50% {
			transform: translate(3px, 1px);
			text-shadow: -3px 1px 0 green;
		}
		55% {
			transform: translate(0);
			text-shadow: 0 0 0 #000;
		}
		75% {
			transform: translate(0);
			text-shadow: 0 0 0 #000;
		}
		80% {
			transform: translate(3px, -1px);
			text-shadow: 3px -1px 0 purple;
		}
		85% {
			transform: translate(0);
			text-shadow: 0 0 0 #000;
		}
		80% {
			transform: translate(-3px, -1px);
			text-shadow: -3px -1px 0 yellow;
		}
		95% {
			transform: translate(0);
			text-shadow: 0 0 0 #000;
		}
	}

	.glitch {
		animation: glitch 2s infinite cubic-bezier(1, 0, 0, 1); /* Adjust duration/speed as needed */
	}
</style>
