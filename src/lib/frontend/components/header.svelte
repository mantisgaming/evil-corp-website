<script lang="ts">
	import { resolve } from '$app/paths';
	import type { PathnameWithSearchOrHash } from '$app/types';
</script>

<nav>
	<div>
		<a href={resolve('/')}
			><img class="logo" alt="SolCorp Logo" src="/favicon.png" />
			<p class="company-name">SolCorp</p></a
		>
	</div>
</nav>

<style lang="scss">
	a {
		text-decoration: none;
		color: black;
		text-transform: capitalize;
		display: flex;
		flex-direction: row;
		align-items: center;
		gap: 1rem;

		p {
			font-size: 2.5rem;
		}
	}

	nav {
		display: flex;
		flex-direction: row;
		justify-content: center;
		align-items: center;
		width: 100%;
		padding: 1rem 3rem;
		background-color: #91ee95;

		& > div {
			display: flex;
			flex-direction: row;
			justify-content: space-between;
			align-items: center;
			width: 100%;
			max-width: 1200px;

			@media screen and (width < 900px) {
				justify-content: center;
			}
		}
	}

	img {
		display: block;
		aspect-ratio: 1 / 1;
		height: 4rem;

		@media screen and (width < 900px) {
			height: 10vw;
		}
	}

	.company-name {
		font-family: onyx;
		letter-spacing: 0.2rem;
		transform: scaleX(110%);
		transform-origin: left;
		text-transform: uppercase;

		@media screen and (width < 900px) {
			font-size: 6vw;
		}
	}
</style>
