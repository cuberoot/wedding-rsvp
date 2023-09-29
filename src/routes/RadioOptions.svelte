<script lang="ts">
	export let options: Record<string, string> = {};
	export let name: string = '';
	export let selected: string | undefined = undefined;
	export let required = false;
</script>

<fieldset class="button-radio">
	{#each Object.entries(options) as [optionName, label]}
		<input type="radio" value={optionName} bind:group={selected} id={optionName} {name} {required} />
		<label for={optionName}>{label}</label>
	{/each}
</fieldset>

<style>
	input {
		position: absolute;
    top: 50%;
    left: 50%;
		opacity: 0;
	}

	fieldset {
		position: relative;
		display: flex;
		flex-direction: column;
		align-items: stretch;
		width: 100%;
		border: none;
    margin: 0;
    padding: 0;
	}

	input + label {
		position: relative;
		padding: 0.5rem 1rem;
		border: 1px solid var(--color-border);
		border-radius: 0.2rem;
		background-color: var(--button-fill);
		margin-bottom: 0.5rem;
	}

	input:checked + label {
		padding: 0.5rem 1rem;
		border: 2px solid var(--color-border);
		background-color: var(--button-fill);
		font-weight: bold;
	}

	input:checked + label::after {
		position: absolute;
		right: 1rem;
		content: '✔';
	}

	input:focus-visible + label {
		outline: 2px solid var(--color-focus);
	}

	input + label:hover {
		background-color: var(--button-fill-hover);
	}
</style>
