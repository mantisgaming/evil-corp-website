<script lang="ts">
	import favicon from '$lib/assets/favicon.svg';
	import FrontendNav from '$lib/components/frontendNav.svelte';

	let { children } = $props();
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
</svelte:head>

<FrontendNav/>
{@render children()}

<style lang="scss">
	
</style>