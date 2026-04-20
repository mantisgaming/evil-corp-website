<script lang="ts">
	import '$lib/backend/assets/index.scss';
	import { getContext } from 'svelte';

	const {
		getUsername,
		logOut
	}: {
		getUsername: () => string;
		logOut: () => void;
	} = getContext('authentication');
</script>

<svelte:head>
	<title>SolCorp | Administration</title>
</svelte:head>

<section>
	<h1>SolCorp Administration</h1>
</section>
<p>Welcome, {getUsername()}</p>
<button onclick={logOut}>Log Out</button>

<style lang="scss">
</style>
