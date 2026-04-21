<script lang="ts">
	import Header from '$lib/frontend/components/header.svelte';
	import Footer from '$lib/frontend/components/footer.svelte';
	import '$lib/frontend/assets/index.scss';
</script>

<svelte:head>
	<title>SolCorp</title>
</svelte:head>

<Header />
<section class="jumbotron">
	<div>
		<div class="title">
			<h1>SolCorp</h1>
			<div class="underline" style="--id:1;"></div>
			<div class="underline" style="--id:0.8;"></div>
			<div class="underline" style="--id:0.6;"></div>
			<div class="underline" style="--id:0.4;"></div>
			<div class="underline" style="--id:0.2;"></div>
		</div>
	</div>
</section>
<section>
	<h2 id="about">About</h2>
	<p>
		Our corporation was founded by our CEO Archibald Geyser in response to the horrific energy
		problems that plague our world. He strives to create a world in which clean energy is provided
		to everybody. He believes all should be empowered to do what they want to do. A company that
		incorporates such honesty and integrity, prioritizing these core values above all else —
		Archibald strives to create such a company. We, as a company, value sustainability and
		innovation. Our mission to allow all people of the world to benefit from clean energy has never
		been more important, with clean energy becoming more rare with time. The technologies that we
		aim to create allow for such opportunities that otherwise may never come to pass. Know that we
		respect people of all backgrounds, and expect to be held accountable for our actions. We aim for
		the betterment of all people.
	</p>
</section>
<section>
	<div class="side-by-side">
		<div>
			<h2 id="another-section">Another Section</h2>
			<p>
				Our corporation was founded by our CEO Archibald Geyser in response to the horrific energy
				problems that plague our world. He strives to create a world in which clean energy is
				provided to everybody. He believes all should be empowered to do what they want to do. A
				company that incorporates such honesty and integrity, prioritizing these core values above
				all else — Archibald strives to create such a company. We, as a company, value
				sustainability and innovation. Our mission to allow all people of the world to benefit from
				clean energy has never been more important, with clean energy becoming more rare with time.
				The technologies that we aim to create allow for such opportunities that otherwise may never
				come to pass. Know that we respect people of all backgrounds, and expect to be held
				accountable for our actions. We aim for the betterment of all people.
			</p>
		</div>
		<div>
			<h2 id="another-section">Another Section</h2>
			<p>
				Our corporation was founded by our CEO Archibald Geyser in response to the horrific energy
				problems that plague our world. He strives to create a world in which clean energy is
				provided to everybody. He believes all should be empowered to do what they want to do. A
				company that incorporates such honesty and integrity, prioritizing these core values above
				all else — Archibald strives to create such a company. We, as a company, value
				sustainability and innovation. Our mission to allow all people of the world to benefit from
				clean energy has never been more important, with clean energy becoming more rare with time.
				The technologies that we aim to create allow for such opportunities that otherwise may never
				come to pass. Know that we respect people of all backgrounds, and expect to be held
				accountable for our actions. We aim for the betterment of all people.
			</p>
		</div>
	</div>
</section>
<section>
	<h2 id="another-section">Another Section</h2>
	<p>
		Our corporation was founded by our CEO Archibald Geyser in response to the horrific energy
		problems that plague our world. He strives to create a world in which clean energy is provided
		to everybody. He believes all should be empowered to do what they want to do. A company that
		incorporates such honesty and integrity, prioritizing these core values above all else —
		Archibald strives to create such a company. We, as a company, value sustainability and
		innovation. Our mission to allow all people of the world to benefit from clean energy has never
		been more important, with clean energy becoming more rare with time. The technologies that we
		aim to create allow for such opportunities that otherwise may never come to pass. Know that we
		respect people of all backgrounds, and expect to be held accountable for our actions. We aim for
		the betterment of all people.
	</p>
</section>
<Footer />

<style lang="scss">
	.title {
		position: relative;
		width: fit-content;
		position: relative;
		display: block;
		transform: scaleX(110%) translateX(-1rem);
		transform-origin: left;
	}

	.underline {
		content: '';
		font-size: 1rem;
		display: block;
		position: relative;
		width: calc(40% + 30% * var(--id));
		top: -1em;
		left: 50%;
		translate: -50%;
		height: calc(1px + 5px * var(--id));
		margin-bottom: calc(8px - 5px * var(--id));
		background-color: white;
		opacity: calc(20% + 60% * var(--id));

		@media screen and (width < 900px) {
			font-size: 1vw;
		}
	}

	.jumbotron {
		padding: 7.5rem 3rem;

		@media screen and (width < 900px) {
			padding: 0 3rem;
			height: 30vw;
		}

		background-image: url('/banner.jpg');
		background-position: center;
		background-size: cover;

		> div {
			display: flex;
			flex-direction: column;
			align-items: start;

			@media screen and (width < 900px) {
				align-items: center;
			}
		}

		h1 {
			font-size: 8rem;
			display: block;
			width: fit-content;
			position: relative;
			text-transform: uppercase;
			letter-spacing: 0.2em;
			padding-left: 1rem;

			@media screen and (width < 900px) {
				font-size: 12vw;
			}
		}
	}

	h2 {
		font-size: 2rem;
		margin-bottom: 2rem;
	}

	p {
		font-size: 1.2rem;
	}

	.side-by-side {
		display: flex;
		flex-direction: row;
		gap: 3rem;
		justify-content: space-between;
		align-items: start;

		@media screen and (width < 900px) {
			flex-direction: column;
		}
	}
</style>
