<script lang="ts">
	import { resolve } from '$app/paths';
	import type { PathnameWithSearchOrHash } from '$app/types';

	const links: {
		title: string;
		path: PathnameWithSearchOrHash;
	}[] = [
		{
			title: 'test',
			path: '/'
		},
		{
			title: 'example',
			path: '/'
		},
		{
			title: 'home',
			path: '/'
		}
	];
</script>

<nav>
	<div>
		<a href={resolve('/')}
			><img class="logo" alt="SolCorp Logo" src="" />
			<p>SolCorp</p></a
		>
		<ul>
			{#each links as link (link)}
				<li>
					<a href={resolve(link.path)}>{link.title}</a>
				</li>
			{/each}
		</ul>
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

	img {
		display: block;
		aspect-ratio: 1 / 1;
		height: 4rem;
	}

	ul {
		padding: 0;
		margin: 0;
		display: flex;
		flex-direction: row;
		list-style-type: none;
		gap: 1rem;

		a {
			display: block;
			padding: 1rem;
			border-radius: 1rem;
			background-color: white;
			transition-duration: 0.5s;
			font-size: unset;

			&:hover {
				background-color: aqua;
			}
		}
	}
</style>
