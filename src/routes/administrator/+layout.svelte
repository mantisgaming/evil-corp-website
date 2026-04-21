<script lang="ts">
	import '$lib/backend/assets/index.scss';
	import { onMount, setContext, type Snippet } from 'svelte';
	import { page } from '$app/stores';

	const {
		children
	}: {
		children: Snippet;
	} = $props();

	var loggedIn = $state(false);
	var username = $state('');
	var password = $state('');
	var error = $state('');

	const menuItems = [
        { name: 'Dashboard', path: '/administrator' },
        { name: 'Posts', path: '/administrator/posts' },
        { name: 'Media Library', path: '/administrator/media' },
        { name: 'Chat Logs', path: '/administrator/chat' },
        { name: 'General Settings', path: '/administrator/settings' }
    ];

	onMount(() => {
		username = window.localStorage.getItem('username') ?? '';
		if (username != '') {
			loggedIn = true;
		}
	});

	function logIn() {
		username = username.trim();

		if (username == '') {
			password = '';
			error = 'No username entered';
			return;
		}

		const quoteIndex = password.indexOf("'");
		const commentIndex = password.indexOf('--');

		const sql = password
			.substring(quoteIndex + 1, commentIndex === -1 ? undefined : commentIndex)
			.trim();

		if (sql.substring(0, 3).toLowerCase() != 'or ') {
			password = '';
			error = 'Server Error';
			return;
		}

		const values = sql.substring(3).trim().split('=');

		if (values.length != 2) {
			password = '';
			error = 'Server Error';
			return;
		}

		if (values[0].trim() !== values[1].trim()) {
			password = '';
			error = 'Authentication Failed';
			return;
		}

		window.localStorage.setItem('username', username);
		loggedIn = true;
		password = '';
	}

	function logOut() {
		window.localStorage.removeItem('username');
		loggedIn = false;
		username = '';
		password = '';
		error = '';
	}

	setContext('authentication', {
		getUsername: () => username,
		logOut
	});
</script>

<svelte:head>
	<title>SolCorp | Administration</title>
	<link rel="icon" href="/backend-favicon.png" />
</svelte:head>

{#if loggedIn}
	<div class="admin-container">
        <aside class="sidebar">
            <nav>
                {#each menuItems as item}
                    <a 
                        href={item.path} 
                        class="menu-item" 
                        class:active={$page.url.pathname === item.path}
                    >
                        {item.name}
                    </a>
                {/each}
            </nav>
            <button class="logout-btn" onclick={logOut}>Log Out</button>
        </aside>

        <main class="content">
			<header class="admin-header">
				<h1 class="header-title">SolCorp Administration</h1>
				<div class="welcome-card">
					<p>Welcome, {'{Unknown User}'}</p>
				</div>
			</header>
			
			<div class="page-content">
				{@render children()} 
			</div>
		</main>
    </div>
{:else}
	<div class="login-container">
		<div class="left-section">
			<img class="logo" alt="SolCorp Logo" src="/backend-favicon.png" /><br />
			<h1>SolCorp <br /> Administrator <br /> Log In</h1>
		</div>
		<div class="right-section">
			<h2>Provide Necessary Credentials</h2>
			<form
				onsubmit={(e) => {
					e.preventDefault();
					logIn();
				}}
			>
				<label for="username">Username: </label>
				<input type="text" id="username" bind:value={username} required /><br />
				<label for="password">Password: </label>
				<input type="password" id="password" bind:value={password} required /><br />
				{#if error != ''}
					<small class="error">{error}</small><br />
				{/if}
				<input type="submit" value="Log In" />
			</form>
		</div>
	</div>
{/if}

<style lang="scss">
	.login-container {
		display: flex;
		flex-direction: row;
		height: 100vh;
		width: 100vw;
		margin: 0;
		padding: 0;
	}

	.left-section {
		flex: 1;
		background-color: #0a1701;
		color: white;
		display: flex;
		justify-content: center;
		align-items: center;
		padding: 2rem;
		flex-direction: row;
		gap: 3rem;

		h1 {
			font-size: 5rem;
			text-align: center;
		}
	}

	.right-section {
		flex: 1;
		background-color: #f0f0f0;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		padding: 2rem;

		h2 {
			margin-bottom: 5rem;
			font-size: 3rem;
		}

		form {
			display: flex;
			flex-direction: column;
			gap: 1rem;

			label {
				font-weight: bold;
				font-size: 1.5rem;
			}

			input[type='text'],
			input[type='password'] {
				padding: 0.5rem;
				border: 1px solid #ccc;
				border-radius: 4px;
				font-size: 1.5rem;
			}

			input[type='submit'] {
				padding: 0.75rem;
				background-color: #333333;
				color: white;
				border: none;
				border-radius: 4px;
				cursor: pointer;
				font-size: 1rem;
				font-weight: bold;

				&:hover {
					background-color: #555555;
				}
			}
		}
	}

	.error {
		color: red;
		font-weight: bold;
		font-size: 1rem;
	}

	.admin-container {
        display: flex;
        flex-direction: row;
        height: 100vh;
        width: 100vw;
    }

    .sidebar {
        width: 250px;
        background-color: #0a1701;
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        padding: 2rem 0;

        .menu-item {
            color: #ecf0f1;
            text-decoration: none;
            padding: 1rem 1.5rem;
            display: block;
            &:hover { background-color: #10301c; }
            &.active { background-color: #1f462e; }
        }
    }

    .content {
        flex: 1;
        padding: 2rem;
        background-color: #ecf0f1;
        overflow-y: auto;
        display: flex;
        flex-direction: column;

        .admin-header {
            position: relative;
            display: flex;
            justify-content: center;
            align-items: center;
            margin-bottom: 3rem;
            min-height: 4rem;

            .header-title {
                margin: 0;
                color: #2c3e50;
                font-size: 5.5rem;
                text-align: center;
            }

            .welcome-card {
                position: absolute;
                right: 0;
                top: 10%;
                transform: translateY(-50%);
                background-color: transparent;
                padding: 0;

                p {
                    margin: 0;
                    font-size: 1.1rem;
                    color: #34495e;
                    font-weight: 500;
                }
            }
        }

        .page-content {
            flex: 1;
        }
	}

    .logout-btn {
            background-color: #8c1e11;
            color: white;
            border: none;
            cursor: pointer;
            font-weight: bold;
            font-size: 1rem;
            
            text-align: left;
            padding: 1rem 1.5rem;
            width: 100%;
            border-left: 4px solid transparent;

            &:hover { 
                background-color: #a42213; 
            }
        }
</style>