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

	var activeMenu = $state('Dashboard');

	const menuItems = ['Dashboard', 'Posts', 'Media Library', 'Chat Logs', 'General Settings'];
</script>

<svelte:head>
	<title>SolCorp | Administration</title>
</svelte:head>

<div class="admin-container">
	<aside class="sidebar">
		<nav>
			{#each menuItems as item}
				<button
					class="menu-item"
					class:active={activeMenu === item}
					onclick={() => (activeMenu = item)}
				>
					{item}
				</button>
			{/each}
		</nav>
	</aside>

	<main class="content">
		<section>
			<h1>SolCorp Administration</h1>
		</section>
		<p>Welcome, {getUsername()}</p>
		<p><strong>Current Section:</strong> {activeMenu}</p>
		<button class="logout-btn" onclick={logOut}>Log Out</button>
	</main>
</div>

<style lang="scss">
	.admin-container {
		display: flex;
		flex-direction: row;
		height: 100vh;
		width: 100vw;
		margin: 0;
		padding: 0;
	}

	.sidebar {
		width: 250px;
		background-color: #0a1701;
		padding: 2rem 0;
		box-shadow: 2px 0 5px rgba(0, 0, 0, 0.1);

		nav {
			display: flex;
			flex-direction: column;
			gap: 0;
		}

		.menu-item {
			background: none;
			border: none;
			padding: 1rem 1.5rem;
			text-align: left;
			font-size: 1rem;
			color: #ecf0f1;
			cursor: pointer;
			transition: all 0.3s ease;
			border-left: 4px solid transparent;

			&:hover {
				background-color: #10301c;
			}

			&.active {
				background-color: #1f462e;
				color: white;
			}
		}
	}

	.content {
		flex: 1;
		padding: 2rem;
		background-color: #ecf0f1;
		overflow-y: auto;

		h1 {
			margin-top: 0;
			color: #2c3e50;
		}

		p {
			font-size: 1.1rem;
			color: #34495e;
		}

		.logout-btn {
			margin-top: 2rem;
			padding: 0.75rem 1.5rem;
			background-color: #e74c3c;
			color: white;
			border: none;
			border-radius: 0px;
			cursor: pointer;
			font-size: 1rem;
			font-weight: bold;
			transition: background-color 0.3s ease;

			&:hover {
				background-color: #c0392b;
			}
		}
	}
</style>
