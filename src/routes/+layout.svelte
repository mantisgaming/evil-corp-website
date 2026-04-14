<script lang="ts">
	import favicon from '$lib/assets/favicon.svg';
	import FrontendNav from '$lib/components/frontendNav.svelte';
	import '$lib/assets/index.scss';
	import FrontendFooter from '$lib/components/frontendFooter.svelte';

	let { children } = $props();
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
</svelte:head>

<FrontendNav/>
{@render children()}
<FrontendFooter/>

<style lang="scss">
	
</style>