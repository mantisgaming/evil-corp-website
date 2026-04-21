<script lang="ts">
	const analytics = [
		{ label: 'Website Visits', value: '2,847', change: '+12%', icon: '📊' },
		{ label: 'Active Users', value: '156', change: '+8%', icon: '👥' },
		{ label: 'Page Views', value: '18,394', change: '+15%', icon: '📄' },
		{ label: 'Avg. Session', value: '4m 32s', change: '+3%', icon: '⏱️' }
	];

	const recentActivity = [
		{ user: '{Unknown User}', action: 'logged in', time: 'just now', icon: '✓' },
		{ user: 'Employee #047', action: 'logged out', time: '2 minutes ago', icon: '✕' },
		{ user: 'Employee #005', action: 'logged in', time: '15 minutes ago', icon: '✓' },
		{ user: 'Employee #152', action: 'logged out', time: '1 hour ago', icon: '✕' },
		{ user: 'Archibald Geyser', action: 'accessed Chat Logs', time: '2 hours ago', icon: '📋' },
		{ user: 'Employee #218', action: 'logged in', time: '3 hours ago', icon: '✓' }
	];

	function getCurrentDate() {
		const date = new Date();
		return date.toLocaleDateString('en-US', {
			weekday: 'long',
			year: 'numeric',
			month: 'long',
			day: 'numeric'
		});
	}
</script>

<svelte:head>
	<title>SolCorp | Dashboard</title>
</svelte:head>

<div class="dashboard-container">
	<div class="dashboard-header">
		<h2 class="current-date">{getCurrentDate()}</h2>
	</div>
	<div class="analytics-grid">
		{#each analytics as item}
			<div class="analytics-card">
				<div class="card-icon">{item.icon}</div>
				<div class="card-content">
					<h3>{item.label}</h3>
					<div class="card-value">{item.value}</div>
					<p class="card-change">{item.change}</p>
				</div>
			</div>
		{/each}
	</div>

	<div class="activity-section">
		<h3>Recent Activity</h3>
		<div class="activity-list">
			{#each recentActivity as activity}
				<div class="activity-item">
					<div
						class="activity-icon {activity.action.includes('logged in')
							? 'login'
							: activity.action.includes('logged out')
								? 'logout'
								: 'action'}"
					>
						{activity.icon}
					</div>
					<div class="activity-details">
						<div class="activity-user">{activity.user}</div>
						<div class="activity-action">{activity.action}</div>
					</div>
					<div class="activity-time">{activity.time}</div>
				</div>
			{/each}
		</div>
	</div>
</div>

<style lang="scss">
	.dashboard-container {
		padding: 0;
	}

	.dashboard-header {
		margin-bottom: 2rem;
		gap: 2rem;

		h2.current-date {
			color: #2c3e50;
			margin-top: 0;
			font-size: 1.5rem;
			gap: 2rem;
		}

		p {
			color: #7f8c8d;
			margin-bottom: 0;
		}
	}

	.analytics-grid {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
		gap: 1.5rem;
		margin-bottom: 2rem;

		.analytics-card {
			background: white;
			border-radius: 8px;
			padding: 1.5rem;
			box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
			display: flex;
			gap: 1rem;
			align-items: flex-start;

			.card-icon {
				font-size: 2rem;
				min-width: 50px;
				text-align: center;
			}

			.card-content {
				flex: 1;

				h3 {
					margin: 0;
					color: #7f8c8d;
					font-size: 0.9rem;
					text-transform: uppercase;
					font-weight: 600;
				}

				.card-value {
					font-size: 1.8rem;
					font-weight: bold;
					color: #2c3e50;
					margin: 0.5rem 0;
				}

				.card-change {
					margin: 0;
					font-size: 0.85rem;
					color: #27ae60;
					font-weight: bold;
				}
			}
		}
	}

	.activity-section {
		background: white;
		border-radius: 8px;
		padding: 1.5rem;
		box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);

		h3 {
			margin-top: 0;
			color: #2c3e50;
			margin-bottom: 1rem;
		}

		.activity-list {
			display: flex;
			flex-direction: column;
			gap: 1rem;

			.activity-item {
				display: flex;
				align-items: center;
				gap: 1rem;
				padding: 1rem;
				background-color: #f8f9fa;
				border-radius: 6px;
				border-left: 4px solid #bdc3c7;

				.activity-icon {
					width: 40px;
					height: 40px;
					border-radius: 50%;
					display: flex;
					align-items: center;
					justify-content: center;
					font-size: 1.2rem;
					font-weight: bold;
					color: white;

					&.login {
						background-color: #27ae60;
					}

					&.logout {
						background-color: #e74c3c;
					}

					&.action {
						background-color: #3498db;
					}
				}

				.activity-details {
					flex: 1;

					.activity-user {
						font-weight: bold;
						color: #2c3e50;
						margin-bottom: 0.25rem;
					}

					.activity-action {
						font-size: 0.9rem;
						color: #7f8c8d;
					}
				}

				.activity-time {
					font-size: 0.85rem;
					color: #95a5a6;
					white-space: nowrap;
				}
			}
		}
	}
</style>
