<script lang="ts">
	import FrontendNav from '$lib/components/frontendNav.svelte';
	import '$lib/assets/index.scss';
	import FrontendFooter from '$lib/components/frontendFooter.svelte';

	let { children } = $props();
</script>

<FrontendNav />
{@render children()}
<FrontendFooter />

<style lang="scss">
</style>
