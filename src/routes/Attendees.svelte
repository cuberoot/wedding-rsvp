<script lang="ts">
  import TextField from "./TextField.svelte";

  export let count = 0;

  function* range(count: number) {
    for (let i = 2; i <= count; i++) {
      yield i;
    }
  }
</script>

{#each range(count) as i}
  <TextField label={`name ${i}`} name={`name-${i}`} required />
{/each}
