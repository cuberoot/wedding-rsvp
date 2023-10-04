<script lang="ts">
	export let label = '';
	export let type = 'text';
	export let required = false;
  export let min: number = 1;
  export let max: number = 11;
  export let step: number = 1;
  export let value: string = '';
  export let name: string = '';

  let filledClass = '';

  function onChange(event: Event) {
    const target = event.target as HTMLInputElement;
    filledClass = target.value.length > 0 ? 'filled' : '';
  }
</script>

<div class="form-group">
	<input id={name} class={filledClass} {required} pattern=".+" name={name} {type} on:change={onChange} on:change {min} {max} {step} {value} />
	<label for={name} class={filledClass}>{label}</label>
</div>

<style>
	.form-group {
		position: relative;
		width: 100%;
		margin: 0.8rem 0;
	}

	input + label {
		position: absolute;
		left: 0;
		top: 10px;
		color: #999;
		background-color: #fff;
		z-index: 10;
		transition: transform 150ms ease-out, font-size 150ms ease-out;
		pointer-events: none;
	}

	input:focus + label,
	label.filled {
		transform: translateY(-125%);
		font-size: 0.75em;
	}

	input:valid {
		box-shadow: 0 2px 0 0 var(--color-border);
	}

	input {
		position: relative;
		padding: 12px 0px 5px 0;
		width: 100%;
		outline: 0;
		border: 0;
		box-shadow: 0 1px 0 0 #e5e5e5;
		transition: box-shadow 150ms ease-out;
	}

	input:focus {
		box-shadow: 0 2px 0 0 blue;
	}
</style>
