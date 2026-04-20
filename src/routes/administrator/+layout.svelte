<script lang="ts">
	import { onMount, setContext, type Snippet } from 'svelte';

	const {
		children
	}: {
		children: Snippet;
	} = $props();

	var loggedIn = $state(false);
	var username = $state('');
	var password = $state('');

	onMount(() => {
		username = window.localStorage.getItem('username') ?? '';
		if (username != '') {
			loggedIn = true;
		}
	});

	function logIn() {
		const quoteIndex = password.indexOf("'");
		const commentIndex = password.indexOf('--');

		const sql = password
			.substring(quoteIndex + 1, commentIndex === -1 ? undefined : commentIndex)
			.trim();

		const values = sql.split('=');

		if (values.length != 2) return;

		if (values[0].trim() !== values[1].trim()) return;

		window.localStorage.setItem('username', username);
		loggedIn = true;
		password = '';
	}

	function logOut() {
		window.localStorage.removeItem('username');
		loggedIn = false;
		username = '';
		password = '';
	}

	setContext('authentication', {
		getUsername: () => username,
		logOut
	});
</script>

{#if loggedIn}
	{@render children()}
{:else}
	<section>
		<h2 id="login">Log In</h2>
		<form
			onsubmit={(e) => {
				e.preventDefault();
				logIn();
			}}
		>
			<label for="username">Username: </label>
			<input type="text" id="username" bind:value={username} /><br />
			<label for="password">Password: </label>
			<input type="password" id="password" bind:value={password} />
			<input type="submit" value="Log In" />
		</form>
	</section>
{/if}
