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
		<h1>
			SolCorp
			<div class="underline" style="--id:1;"></div>
			<div class="underline" style="--id:0.8;"></div>
			<div class="underline" style="--id:0.6;"></div>
			<div class="underline" style="--id:0.4;"></div>
			<div class="underline" style="--id:0.2;"></div>
		</h1>
	</div>
</section>
<section>
	<h2 id="about">About</h2>
	<p>Insert any information about the company...</p>
</section>
<section>
	<h2 id="another-section">Another Section</h2>
	<p>Insert any information about the company...</p>
</section>
<section>
	<h2 id="another-section">Another Section</h2>
	<p>Insert any information about the company...</p>
</section>
<Footer />

<style lang="scss">
	.jumbotron {
		padding: 7.5rem 0;

		background-image: url('/banner.jpg');
		background-position: center;
		background-size: cover;

		h1 {
			font-size: 8rem;
			display: block;
			width: fit-content;
			position: relative;

			.underline {
				content: '';
				display: block;
				position: relative;
				width: calc(40% + 30% * var(--id));
				top: -1rem;
				left: 50%;
				translate: -50%;
				height: calc(1px + 5px * var(--id));
				margin-bottom: calc(8px - 5px * var(--id));
				background-color: white;
				opacity: calc(20% + 60% * var(--id));
			}
		}
	}
</style>
