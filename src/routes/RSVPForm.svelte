<script lang="ts">
	import { fade } from 'svelte/transition';
  import TextField from './TextField.svelte';

	let coming: 'coming' | 'no-coming' | undefined = undefined;
	let hasName = false;

	function nameChange(event: Event) {
		const target = event.target as HTMLInputElement;
		hasName = target.value.length > 0;
		event.preventDefault();
		event.stopPropagation();
	}
</script>

<div id="rsvp-form">
	<form method="POST">
		<button type="submit" disabled style="display: none" aria-hidden="true" />

		<TextField label="full name" on:change={nameChange} />

		{#if hasName}
			<fieldset transition:fade class="button-radio">
				<input type="radio" value="coming" bind:group={coming} id="coming" name="coming" />
				<label for="coming">I am coming</label>
				<input type="radio" id="not-coming" bind:group={coming} name="not-coming" value="not-coming" />
				<label for="not-coming">I can't make it</label>
			</fieldset>
		{/if}

		{#if coming === 'coming'}
			<div transition:fade id="coming-fields" class="field-grid">
				<label for="name">Name</label>
				<input id="name" name="name" type="text" />
				<label for="email">Email</label>
				<input id="email" name="email" type="email" />
			</div>
		{/if}

		{#if coming !== undefined}
			<button transition:fade formaction="?/register">RSVP</button>
		{/if}
	</form>
</div>

<style>
	#rsvp-form {
		max-width: 80%;
		min-width: 300px;
		padding: 50px 30px 50px 30px;
		margin: 50px auto;
		background-color: #ffffff;
		border-radius: 5px;
		box-shadow: 0 15px 35px rgba(50, 50, 93, 0.1), 0 5px 15px rgba(0, 0, 0, 0.07);
	}

	fieldset {
		border: none;
		max-width: 300px;
	}

	form {
		display: flex;
		position: relative;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		width: 100%;
		font-size: 1.3rem;
	}

	fieldset.button-radio {
		display: flex;
		flex-direction: column;
		width: 100%;
	}

	fieldset.button-radio > input[type='radio'] {
		display: none;
	}

	fieldset.button-radio > input[type='radio'] + label {
		padding: 0.5rem 1rem;
		border: 1px solid var(--color-border);
		border-radius: 0.2rem;
		background-color: var(--button-fill);
		margin-bottom: 0.5rem;
	}

	fieldset.button-radio > input[type='radio']:checked + label {
		position: relative;
		font-weight: bold;
		background-color: var(--button-fill-hover);
		border-width: 2px;
	}

	fieldset.button-radio > input[type='radio']:checked + label::after {
		position: absolute;
		right: 1rem;
		content: '✔';
	}

	fieldset.button-radio > input[type='radio'] + label:hover {
		background-color: var(--button-fill-hover);
	}

	.field-grid {
		display: grid;
		align-items: last baseline;
		grid-template-columns: auto 1fr;
		grid-gap: 1rem;
	}
</style>
