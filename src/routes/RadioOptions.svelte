<script lang="ts">
  export let options: Record<string, string> = {};
  export let name: string = '';
  export let selected: string | undefined = undefined;
</script>

<fieldset class="button-radio">
  {#each Object.entries(options) as [optionName, label]}
    <input type="radio" value={optionName} bind:group={selected} id={optionName} {name} />
    <label for={optionName}>{label}</label>
  {/each}
</fieldset>

<style>
	input {
		position: absolute;
		opacity: 0;
	}

  fieldset {
    position: relative;
    display: flex;
    flex-direction: column;
    align-items: stretch;
    width: 100%;
    border: none;
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
