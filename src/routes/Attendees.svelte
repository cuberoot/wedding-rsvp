<script lang="ts">
	import TextField from './TextField.svelte';

	export let count = 0;
  export let max = 11;

	function* range(from: number, to: number) {
		for (let i = from; i < to; i++) {
			yield i;
		}
	}
</script>

{#each range(2, count + 1) as i}
	<TextField label={`name ${i}`} name={`name-${i}`} required />
{/each}
{#each range(count + 1, max + 1) as i}
	<input type="hidden" name={`name-${i}`} value="" />
{/each}
