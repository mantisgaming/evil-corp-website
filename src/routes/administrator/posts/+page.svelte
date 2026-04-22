<script lang="ts">
	let posts = $state([
		{
			title: 'IMPORTANT ANNOUNCEMENT - REGARD WITH CARE',
			author: 'Archibald Geyser',
			content:
				'hello, evEryone is doinG a gOod Job. haPpy day off, Go reSt and enJoy yourselves! Please eXplore our Free excitingG new Help and acTivity paGE. i Like Just  sPending  free time parKing on oPen roads And watcHing caRs rAce by. drinK lots of watEr aNd have a Quiet evening, and a grab a Jacket in case rain faLls. I Need a HaNd helPinG savE files befoRe everyBody leaves toNight For the long weekend, so Answer Quickly. SPend your eXtra time well!',
			date: '2 hours ago'
		},
		{
			title: 'Plans For SolCorp Expansion',
			author: 'Employee #005',
			content:
				'How does this sound for the updated website?\n"Our corporation was founded by our CEO Archibald Geyser in response to the horrific energy problems that plague our world. He strives to create a world in which clean energy is provided to everybody. He believes all should be empowered to do what they want to do. A company that incorporates such honesty and integrity, prioritizing these core values above all else — Archibald strives to create such a company. We, as a company, value sustainability and innovation. Our mission to allow all people of the world to benefit from clean energy has never been more important, with clean energy becoming more rare with time. The technologies that we aim to create allow for such opportunities that otherwise may never come to pass. Know that we respect people of all backgrounds, and expect to be held accountable for our actions. We aim for the betterment of all people."\nLet me know if you have any feedback!',
			date: '5 hours ago'
		}
	]);

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

<div class="posts-page-container">
	<h2 class="current-date">{getCurrentDate()}</h2>

	<div class="posts-scroll-area">
		{#each posts as post}
			<article class="post-box">
				<div class="post-header">
					<h2>{post.title}</h2>
					<span class="post-meta">By <strong>{post.author}</strong> • {post.date}</span>
				</div>
				<div class="post-body">
					<p>{post.content}</p>
				</div>
			</article>
		{/each}
	</div>
</div>

<style lang="scss">
	.posts-page-container {
		display: flex;
		flex-direction: column;
		align-items: flex-start;
		margin-left: 0;
		padding: 2rem;
		font-family: 'Inter', sans-serif;

		h2.current-date {
			color: #2c3e50;
			margin-top: 0;
			margin-bottom: 4rem;
			font-size: 1.5rem;
		}

		p {
			color: #7f8c8d;
			margin-bottom: 0;
		}

		.page-header {
			margin-bottom: 2rem;
			border-bottom: 2px solid #2c3e50;
			padding-bottom: 1rem;

			h1 {
				color: #2c3e50;
				margin: 0;
				font-size: 2.5rem;
			}
			p {
				color: #7f8c8d;
				margin-top: 0.5rem;
				font-style: italic;
			}
		}
	}

	.posts-scroll-area {
		display: flex;
		flex-direction: column;
		gap: 2rem;
		max-height: 80vh;
		overflow-y: auto;
		padding-right: 1rem;
	}

	.post-box {
		background: white;
		border: 1px solid #bdc3c7;
		border-radius: 8px;
		padding: 1.5rem;
		box-shadow: 0 4px 6px rgba(0, 0, 0, 0.05);
		transition: transform 0.2s ease;

		&:hover {
			transform: translateY(-2px);
			border-color: #3498db;
		}

		.post-header {
			margin-bottom: 1rem;
			h2 {
				margin: 0;
				color: #2c3e50;
				font-size: 1.4rem;
			}
			.post-meta {
				font-size: 0.85rem;
				color: #95a5a6;
			}
		}

		.post-body {
			p {
				color: #34495e;
				line-height: 1.6;
				margin-bottom: 1rem;
			}
		}
	}
</style>
