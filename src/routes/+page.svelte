<script>
	import RSVPForm from './RSVPForm.svelte';
	import flowers from '$lib/images/Flowers.webp';
	import flowers_fallback from '$lib/images/Flowers.png';
</script>

<svelte:head>
	<title>Home</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>

<section>
	<h1>
		<span class="flowers">
			<picture>
				<source srcset={flowers} type="image/webp" />
				<img src={flowers_fallback} alt="Welcome" />
			</picture>
		</span>

		Wedding RSVP
	</h1>

	<RSVPForm />
</section>

<style>
	section {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		flex: 0.6;
	}

	h1 {
		width: 100%;
	}

	.flowers {
		display: block;
		position: relative;
		width: 60%;
		height: 0;
		padding: 0 0 calc(60% * 1008 / 1060) 0;
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
