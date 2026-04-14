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
		<a href={resolve('/')}>SolCorp</a>
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
</style>
