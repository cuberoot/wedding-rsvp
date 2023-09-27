<script lang="ts">
	export let group = '';
	export let label = '';
	export let value = '';
	export let name = '';
</script>

<input type="radio" {value} bind:group id={value} {name} />
<label for={value}>{label}</label>

<style>
	input {
		position: absolute;
		opacity: 0;
	}

	input + label {
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
