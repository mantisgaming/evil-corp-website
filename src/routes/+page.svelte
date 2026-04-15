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
	<h1>SolCorp</h1>
	<p>Insert tagline here...</p>
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
		color: white;
		position: relative;
		background-color: unset;

		text-align: center;

		::before {
			content: '';
			position: absolute;
			top: 0;
			bottom: 0;
			left: 0;
			right: 0;
			background-image: url('/placeholder-banner.jpg');
			background-attachment: fixed;
			background-position: top;
			background-size: cover;
			z-index: -1;
			filter: blur(1px) brightness(50%);
		}
	}
</style>
