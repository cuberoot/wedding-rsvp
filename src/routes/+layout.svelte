<script>
	import './styles.css';
</script>

<svelte:head>
	<link rel="stylesheet" href="https://use.typekit.net/zjc8ces.css">
</svelte:head>

<div class="app">
	<main>
		<slot />
	</main>
</div>

<style>
	.app {
		display: flex;
		flex-direction: column;
		min-height: 100vh;
	}

	main {
		flex: 1;
		display: flex;
		flex-direction: column;
		width: 100%;
		margin: 0 auto;
		box-sizing: border-box;
	}
</style>
