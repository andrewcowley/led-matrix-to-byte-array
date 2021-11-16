<script>
  import Button from "./Button.svelte";
  import Grid from "./Grid.svelte";
  import ByteArray from "./ByteArray.svelte";

  $: grid = [
    [false, false, false, true, false, false, false, false],
    [false, false, false, false, false, false, false, false],
    [false, false, false, false, false, false, false, false],
    [false, false, false, false, false, false, false, false],
    [false, false, false, false, false, false, false, false],
    [false, false, false, false, false, false, false, false],
    [false, false, false, false, false, false, false, false],
    [false, false, false, false, false, false, false, false]
  ];

  $: byteArray = grid.map(item => {
    const binaryNumber = item.map(value => +value).join("");
    const hexadecimalNumber = parseInt(`${binaryNumber}`, 2).toString(16);
    return `0x${hexadecimalNumber}`;
  });

  function handleClick (evt) {
    console.log('hi', evt)
  }

  function handleCheckBoxClick (evt) {
    const {row, box} = evt.detail
    let newArray = grid.map(function(arr) {
    return arr.slice();
    });
    let removed = newArray[row].splice(box, 1, !newArray[row][box])
    console.log(newArray, removed)
    grid = newArray;

  }
</script>

<style>
  main {
    font-family: sans-serif;
    text-align: center;
  }
</style>

<main>
	<h1>Grid of 0 or 1s</h1>
	
  <Grid grid={grid} on:boxclick={handleCheckBoxClick}/>
  <Button on:reset={handleClick}/>
  {grid}
  <ByteArray byteArray={byteArray}/>
</main>