<script>
  import Button from "./Button.svelte";
  import Grid from "./Grid.svelte";
  import ByteArray from "./ByteArray.svelte";
</script>

<style>
  main {
    font-family: sans-serif;
    text-align: center;
  }
</style>

<main>
	<h1>Grid of 0 or 1s</h1>
	
  <Grid />
  <ByteArray />
</main>