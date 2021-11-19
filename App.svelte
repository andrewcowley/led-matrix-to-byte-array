<script>
  import Button from "./Button.svelte";
  import Grid from "./Grid.svelte";
  import ByteArray from "./ByteArray.svelte";
  import {chars} from './chars';

  let key;
	let keyCode;

  $: grid = [
    [false, false, false, false, false, false, false, false],
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

  function handleCheckBoxClick (evt) {
    const {row, box} = evt.detail
    let newArray = grid.map(function(arr) {
    return arr.slice();
    });
    let removed = newArray[row].splice(box, 1, !newArray[row][box])
    console.log(newArray, removed)
    grid = newArray;

  }

  function handleResetClick () {
    grid = grid.map((row)=> {
      return row.map((box) =>  false)
    })
  }

  function handleKeydown(event) {
		// TODO handle modified keys in chars object
    key = event.key;
    const binaryArray = chars[key].map((item)=>{
      return parseInt(item, 16).toString(2).padStart(8, '0').split('').reverse()
    }).map((row) => {
      return row.map((box)=> {
        return !!+box;
      })
    })
    grid = binaryArray;
	}

</script>

<style>
  main {
    font-family: sans-serif;
    text-align: center;
  }
</style>

<svelte:window on:keydown={handleKeydown}/>

<main>
	<h1>Grid of 0 or 1s</h1>
  <Grid grid={grid} on:boxclick={handleCheckBoxClick}/>
  <Button on:click={handleResetClick}/>
  <ByteArray byteArray={byteArray}/>
</main>