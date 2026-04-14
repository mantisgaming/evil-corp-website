<script lang="ts">
	import { resolve } from '$app/paths';
	import type { PathnameWithSearchOrHash } from '$app/types';

	const links: {
		title: string;
		path: PathnameWithSearchOrHash;
	}[] = [
		{
			title: 'home',
			path: '/'
		}
	];
</script>

<nav>
	<a href={resolve("/")}><img class="logo" alt="SolCorp Logo" src="" /></a>
	<ul>
		{#each links as link (link)}
			<li>
				<a href={resolve(link.path)}>{link.title}</a>
			</li>
		{/each}
	</ul>
</nav>

<style lang="scss">
	
</style>