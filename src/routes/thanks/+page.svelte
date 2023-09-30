<script lang=ts>
	import background from '$lib/images/background.webp';
</script>

<svelte:head>
	<title>Thank you!</title>
	<meta name="description" content="Thank you" />
</svelte:head>

<div class="container">
  <div class="text-box">
    <h1>Thank you!</h1>
    <p>
      Thank you for your response!
    </p>
  </div>
</div>

<style>
  :global(body) {
    background-image: url("/background.jpg");
    background-image: image-set("/background.webp", "/background.jpg");
    background-size: cover;
  }

  .container {
    display: flex;
    justify-content: center;
    align-items: center;
    flex: 1;
  }

  .text-box {
    background-color: white;
    text-align: center;
    align-self: center;
    padding: 2rem;
    border-radius: 1rem;
  }
</style>

