<script lang="ts">
	import '$lib/backend/assets/index.scss';
	import { getContext, onMount } from 'svelte';

	const {
		getUsername,
		logOut
	}: {
		getUsername: () => string;
		logOut: () => void;
	} = getContext('authentication');

	var activeMenu = $state('Dashboard');

	const menuItems = ['Dashboard', 'Posts', 'Media Library', 'Chat Logs', 'General Settings'];

	const userGroups = [
        { role: "Administrator", color: "#e74c3c", members: ["Archibald Geyser"] },
        { role: "Moderators", color: "#f1c40f", members: ["Employee #005", "Employee #047"] },
        { role: "Users", color: "#95a5a6", members: ["Employee #025", "Employee #088", 
			"Employee #093", "Employee #127", "Employee #152", "Employee #171", 
			"Employee #202", "Employee #213", "Employee #218", "{Unknown User}"] }
    ];

	let mediaItemsList = $state([
        {
            title: "Invention Blueprint - Fragment #2",
            postedBy: "Employee #152",
            time: "2 hours ago",
            imageUrl: '/temp_bike_image.jpg',
            description: "The most recent blueprint piece found by faculty. Will be deleted soon, so make sure to download and preserve."
        }
    ]);

	let chatMessages = $state([
		{
			name: "Employee #047",
			profile: "👤",
			message: "Keep any conversations like this verbel, and make sure the blueprint is deleted after being up for 24 hours. The less of a trace we leave, the better.",
			time: "2 hours ago"
		},
		{
			name: "Employee #093",
			profile: "👤",
			message: "Upload them to the Media Library tab. Don't worry, the public won't be able to see them, only us.",
			time: "3 hours ago"
		},
		{
			name: "Employee #152",
			profile: "👤",
			message: "Where are we storing pieces of blueprints we've found? I was told to put them here in the backend somewhere.",
			time: "3 hours ago"
		}
	]);

	let timer1: NodeJS.Timeout | null = null;
	let timer2: NodeJS.Timeout | null = null;
	let timersStarted = $state(false);

	$effect(() => {
		if (activeMenu === 'Chat Logs' && !timersStarted) {
			timersStarted = true;

			timer1 = setTimeout(() => {
				chatMessages = [
					{
						name: "Employee #218",
						profile: "👤",
						message: "Who is {Unknown User}? I didn't know we could have invalid names like that.",
						time: "just now"
					},
					...chatMessages
				];
			}, 15000);

			timer2 = setTimeout(() => {
				chatMessages = [
					{
						name: "Employee #005",
						profile: "👤",
						message: "We shouldn't be able to. Someone notify Archibald about this immediately.",
						time: "just now"
					},
					...chatMessages
				];
			}, 20000);
		}
	});

	onMount(() => {
		return () => {
			if (timer1) clearTimeout(timer1);
			if (timer2) clearTimeout(timer2);
		};
	});

	function getCurrentDate() {
		const date = new Date();
		return date.toLocaleDateString('en-US', { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' });
	}
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
					onclick={() => activeMenu = item}
				>
					{item}
				</button>
			{/each}
		</nav>
		<button class="logout-btn" onclick={logOut}>Log Out</button>
	</aside>

	<main class="content">
		<section>
			<h1>SolCorp Administration</h1>
		</section>
		<div class="welcome-card">
			<p>Welcome, {'{Unknown User}'}</p>
		</div>
		
		{#if activeMenu === 'Chat Logs'}
			<div class="chat-logs-container">
				<p class="current-date">{getCurrentDate()}</p>
				
				<div class="chat-layout-wrapper">
					<div class="chat-boxes">
						{#each chatMessages as chat}
							<div class="chat-box">
								<div class="profile-header">
									<div class="profile-info">
										<span class="profile-icon">{chat.profile}</span>
										<span class="profile-name">{chat.name}</span>
									</div>
									<span class="chat-time">{chat.time}</span>
								</div>
								<p class="chat-message">{chat.message}</p>
							</div>
						{/each}
					</div>

					<aside class="user-list-sidebar">
						{#each userGroups as group}
							<div class="user-group">
								<h3 style="color: {group.color}">{group.role} — {group.members.length}</h3>
								{#each group.members as member}
									<div class="user-item">
										<span class="user-status-icon">👤</span>
										<span class="user-name">{member}</span>
									</div>
								{/each}
							</div>
						{/each}
					</aside>
				</div>
			</div>
		{/if}
		{#if activeMenu === 'Media Library'}
            <div class="media-library-container">
                <p class="current-date">{getCurrentDate()}</p>
                
                <div class="media-grid">
                    {#each mediaItemsList as item}
                        <div class="media-card">
                            <div class="media-image-wrapper">
                                <img src={item.imageUrl} alt={item.title} />
                            </div>
                            <div class="media-info">
                                <h3>{item.title}</h3>
                                <p class="media-meta">Posted by <strong>{item.postedBy}</strong> • {item.time}</p>
                                <p class="media-description">{item.description}</p>
                            </div>
                        </div>
                    {/each}
                </div>
            </div>
        {/if}
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
		display: flex;
		flex-direction: column;
		justify-content: space-between;

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
		position: relative;

		section {
			background-color: transparent !important;
			padding: 0;
			display: flex;
			justify-content: center;
			align-items: flex-start;
			margin-bottom: 2rem;
		}

		h1 {
			margin: 0;
			color: #2c3e50;
			text-align: center;
		}

		p {
			font-size: 1.1rem;
			color: #34495e;
		}

		.welcome-card {
			position: absolute;
			top: 2rem;
			right: 2rem;
			background-color: #ecf0f1;
			padding: 0rem;
			color: #34495e;

			p {
				margin: 0rem 0;
				font-size: 1.1rem;
			}
		}

		.media-library-container {
            padding-top: 1rem;

            .current-date {
                font-size: 0.95rem;
                color: #7f8c8d;
                margin-bottom: 2rem;
            }

            .media-grid {
                display: grid;
                grid-template-columns: repeat(auto-fill, minmax(350px, 1fr));
                gap: 2rem;
            }

            .media-card {
                background-color: white;
                border: 1px solid #bdc3c7;
                border-radius: 4px;
                overflow: hidden;
                box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
                transition: transform 0.2s ease;

                &:hover {
                    transform: translateY(-4px);
                }

                .media-image-wrapper {
                    width: 100%;
                    height: 200px;
                    background-color: #2c3e50;
                    display: flex;
                    justify-content: center;
                    align-items: center;

                    img {
                        width: 100%;
                        height: 100%;
                        object-fit: cover;
                    }
                }

                .media-info {
                    padding: 1.5rem;

                    h3 {
                        margin: 0 0 0.5rem 0;
                        color: #2c3e50;
                        font-size: 1.1rem;
                    }

                    .media-meta {
                        font-size: 0.85rem;
                        color: #95a5a6;
                        margin-bottom: 1rem;
                    }

                    .media-description {
                        font-size: 0.9rem;
                        color: #34495e;
                        line-height: 1.4;
                        margin: 0;
                    }
                }
            }
        }

		.chat-logs-container {
			padding-top: 1rem;

			.current-date {
				font-size: 0.95rem;
				color: #7f8c8d;
				margin-bottom: 2rem;
			}

			.chat-layout-wrapper {
				display: flex; 
				flex-direction: row;
				align-items: flex-start;
				gap: 2rem;
				width: 100%;
        	}

			.chat-boxes {
				display: flex;
				flex-direction: column;
				gap: 1.5rem;
				max-width: calc(120% - 250px);

				.chat-box {
					background-color: white;
					border: 1px solid #bdc3c7;
					border-radius: 4px;
					padding: 1.5rem;
					box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);

					.profile-header {
						display: flex;
						align-items: center;
						justify-content: space-between;
						margin-bottom: 0.5rem;

						.profile-info {
							display: flex;
							align-items: center;
							gap: 0.75rem;

							.profile-icon {
								font-size: 1.5rem;
							}

							.profile-name {
								font-weight: bold;
								color: #2c3e50;
								font-size: 1rem;
							}
						}

						.chat-time {
							font-size: 0.85rem;
							color: #95a5a6;
						}
					}

					.chat-message {
						color: #34495e;
						margin: 0;
						font-size: 0.95rem;
						line-height: 1.5;
					}
				}
			}
		}

		.user-list-sidebar {
			width: 400px;
			background-color: #f8f9fa;
			border-radius: 4px;
			padding: 1rem;
			border: 1px solid #bdc3c7;
			position: sticky;
			top: 0;

        .user-group {
            margin-bottom: 1.5rem;

            h3 {
                font-size: 1.2rem;
                text-transform: uppercase;
                letter-spacing: 1px;
                margin-bottom: 0.5rem;
                border-bottom: 1px solid #eee;
                padding-bottom: 0.25rem;
            }
        }

        .user-item {
            display: flex;
            align-items: center;
            gap: 0.5rem;
            padding: 0.25rem 0;
            
				.user-status-icon {
					font-size: 0.9rem;
					opacity: 0.7;
				}

				.user-name {
					font-size: 1.2rem;
					color: #2c3e50;
				}
        	}
    	}
	}

	.sidebar .logout-btn {
		background: none;
		border: none;
		padding: 1rem 1.5rem;
		text-align: left;
		font-size: 1rem;
		color: white;
		cursor: pointer;
		transition: all 0.3s ease;
		border-left: 4px solid transparent;
		background-color: #8c1e11;
		margin: 0;
		width: 100%;
		font-weight: bold;

		&:hover {
			background-color: #9f1c11;
		}
	}
</style>