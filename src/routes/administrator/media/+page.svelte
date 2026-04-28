<script lang="ts">
	let mediaItemsList = $state([
		{
			title: 'Uncovered Blueprint Piece',
			postedBy: 'Employee #152',
			time: '2 hours ago',
			imageUrl: '/gNuWqUUaSD.png',
			link: 'https://users.wpi.edu/~lwjohnson/gNuWqUUaSD.html',
			description:
				'The most recent blueprint piece found by faculty. Will be deleted soon, so make sure to download and preserve.'
		}
	]);

	let hoveredImage = $state(null);

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

<div class="media-library-container">
	<h2 class="current-date">{getCurrentDate()}</h2>

	<div class="media-layout-wrapper">
		<div class="media-grid">
			{#each mediaItemsList as item}
				<div
					class="media-card"
					onmouseenter={() => (hoveredImage = item.imageUrl)}
					onmouseleave={() => (hoveredImage = null)}
					role="presentation"
				>
					<div class="media-image-wrapper">
						<img src={item.imageUrl} alt={item.title} />
					</div>
					<div class="media-info">
						<h3>
							<a href={item.link} target="_blank" class="title-link">{item.title}</a>
						</h3>
						<p class="media-meta">Posted by <strong>{item.postedBy}</strong> • {item.time}</p>
						<p class="media-description">{item.description}</p>
					</div>
				</div>
			{/each}
		</div>

		<aside class="enlarged-preview-sidebar">
			{#if hoveredImage}
				<div class="preview-frame">
					<img src={hoveredImage} alt="Enlarged Preview" />
				</div>
			{/if}
		</aside>
	</div>
</div>

<style lang="scss">
	.media-library-container {
		padding-top: 1rem;

		h2.current-date {
			color: #2c3e50;
			margin-top: 0;
			font-size: 1.5rem;
		}

		p {
			color: #7f8c8d;
			margin-bottom: 0;
		}

		.current-date {
			font-size: 0.95rem;
			color: #7f8c8d;
			margin-bottom: 2rem;
		}

		.media-layout-wrapper {
			display: flex;
			flex-direction: row;
			gap: 0.5rem;
			align-items: flex-start;
			max-width: 1200px;
		}

		.media-grid {
			flex: 1;
			display: grid;
			grid-template-columns: repeat(auto-fill, minmax(330px, 1fr));
			gap: 2rem;
		}

		.media-card {
			background-color: white;
			border: 1px solid #bdc3c7;
			border-radius: 4px;
			overflow: hidden;
			box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
			cursor: crosshair;

			.media-image-wrapper {
				width: 100%;
				height: 180px;
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
					font-weight: bold;
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
				}
			}
		}

		.enlarged-preview-sidebar {
			width: 500px;
			flex-shrink: 0;
			position: sticky;
			top: 0;

			transform: translateX(-100px) scale(1.2);

			.preview-frame {
				width: 100%;
				border: 2px solid #2c3e50;
				background-color: #000;
				border-radius: 8px;
				overflow: hidden;
				box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);

				img {
					width: 100%;
					display: block;
					height: auto;
				}
			}
		}
	}
</style>