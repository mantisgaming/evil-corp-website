<script lang="ts">
	let password = $state('');
	let isUnlocked = $state(false);

	function checkPassword() {
		if (password === 'Bobert') {
			isUnlocked = true;
		} else {
			password = '';
			alert('Incorrect password. Try again.');
		}
	}
</script>

<svelte:head>
	<title>SolCorp | Settings</title>
</svelte:head>

<div class="settings-container">
	{#if !isUnlocked}
		<div class="restricted-section">
			<h2>Access Restricted</h2>
			<p>User is lacking in permissions. Can bypass this with a password provided by Moderator or Administrator.</p>
			
			<div class="password-box">
				<input 
					type="password" 
					bind:value={password}
					placeholder="Enter password"
					onkeydown={(e) => {
						if (e.key === 'Enter') checkPassword();
					}}
				/>
				<button onclick={checkPassword}>Unlock</button>
			</div>
		</div>
	{:else}
		<div class="blueprint-section">
			<h2>Bike Blueprint #3</h2>
			<div class="blueprint-content">
				<img src="/temp_bike_image.jpg" alt="Bike Blueprint" />
			</div>
		</div>
	{/if}
</div>

<style lang="scss">
	.settings-container {
		display: flex;
		justify-content: center;
		align-items: center;
		min-height: 65vh;
		background-color: #ecf0f1;
		padding: 2rem;
	}

	.restricted-section {
		text-align: center;
		background: white;
		padding: 3rem;
		border-radius: 8px;
		box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
		max-width: 500px;

		h2 {
			color: #e74c3c;
			font-size: 2rem;
			margin-bottom: 1rem;
		}

		p {
			color: #34495e;
			font-size: 1.1rem;
			margin-bottom: 2rem;
		}

		.password-box {
			display: flex;
			flex-direction: column;
			gap: 1rem;

			input {
				padding: 0.75rem;
				font-size: 1rem;
				border: 2px solid #bdc3c7;
				border-radius: 4px;
				transition: border-color 0.3s ease;

				&:focus {
					outline: none;
					border-color: #083e2a;
				}
			}

			button {
				padding: 0.75rem;
				background-color: #083e2a;
				color: white;
				border: none;
				border-radius: 4px;
				font-size: 1rem;
				font-weight: bold;
				cursor: pointer;
				transition: background-color 0.3s ease;

				&:hover {
					background-color: #0c543a;
				}
			}
		}
	}

	.blueprint-section {
		background: white;
		padding: 2rem;
		border-radius: 8px;
		box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
		max-width: 800px;

		h2 {
			color: #2c3e50;
			font-size: 2rem;
			margin-bottom: 2rem;
			text-align: center;
		}

		.blueprint-content {
			background-color: #f8f9fa;
			border: 2px solid #0a1701;
			border-radius: 4px;
			padding: 1.5rem;
			overflow-x: auto;

			pre {
				color: #0a1701;
				font-family: 'Courier New', monospace;
				font-size: 0.9rem;
				line-height: 1.4;
				margin: 0;
				white-space: pre-wrap;
				word-wrap: break-word;
			}
		}
	}
</style>
