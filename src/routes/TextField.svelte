<script>
  export let label = '';
</script>

<div class="form-group">
  <input id="name" required pattern=".+" name="name" type="text" on:change />
  <label class="text-label" for="name">{ label }</label>
  <div class="hint">press <strong>Enter</strong> ↵</div>
</div>

<style>
	.form-group {
		position: relative;
    width: 100%;
	}

	input[type='text'] + label {
		position: absolute;
		left: 0;
		top: 10px;
		color: #999;
		background-color: #fff;
		z-index: 10;
		transition: transform 150ms ease-out, font-size 150ms ease-out;
    pointer-events: none;
	}

	input[type='text']:focus + label, input[type='text']:valid + label {
		transform: translateY(-125%);
		font-size: 0.75em;
	}

  input[type='text']:valid {
		box-shadow: 0 2px 0 0 var(--color-border);
  }

	input[type='text'] {
		position: relative;
		padding: 12px 0px 5px 0;
		width: 100%;
		outline: 0;
		border: 0;
		box-shadow: 0 1px 0 0 #e5e5e5;
		transition: box-shadow 150ms ease-out;
	}

	input[type='text']:focus {
		box-shadow: 0 2px 0 0 blue;
	}

  .hint {
    font-size: 0.8rem;
    color: #999;
    margin-top: 0.5rem;
    text-align: right;
    pointer-events: none;
  }
</style>
