<script>
	import RSVPForm from './RSVPForm.svelte';
	import flowers from '$lib/images/Flowers.webp';
	import flowers_fallback from '$lib/images/Flowers.png';
</script>

<svelte:head>
	<title>Wedding RSVP</title>
	<meta name="description" content="Matt and Gemma's wedding RSVP" />
</svelte:head>

<section>
	<h1>
		<span class="flowers">
			<picture>
				<source srcset={flowers} type="image/webp" />
				<img src={flowers_fallback} alt="Welcome" />
			</picture>
		</span>

		matthieu &amp; gemma
	</h1>
  <h3>wedding RSVP</h3>

	<RSVPForm />
</section>

<style>
	section {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		flex: 0.6;
    padding: 1rem;
	}

	h1 {
		width: 100%;
	}

	.flowers {
		display: block;
		position: relative;
		width: 50%;
		height: auto;
		padding: 0 0 calc(50% * 1008 / 1060) 0;
		margin: 0 auto;
	}

	.flowers img {
		position: absolute;
		width: 100%;
		height: 100%;
		top: 0;
		display: block;
	}
</style>
