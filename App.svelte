<script>
  import Button from "./Button.svelte";
  import Grid from "./Grid.svelte";
  import ByteArray from "./ByteArray.svelte";
  import {chars} from './chars';

  console.log('butts', chars.A)

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
		key = event.key;
    let binaryArray = [];
    if (chars[key]) {
      // binaryArray = chars[key].map((item)=> `${item}`.toString(2).)
      chars[key].forEach((row) => {
        binaryArray.push(parseInt(row, 16).toString(2).padStart(8, '0').split(''))
      })
    }
    console.log(binaryArray)
    const boolArray = binaryArray.map((row)=> {
      return row.map((item) => !!+item)
    })
    grid = boolArray;
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
	{key}{keyCode}
  <Grid grid={grid} on:boxclick={handleCheckBoxClick}/>
  <Button on:click={handleResetClick}/>
  {grid}
  <ByteArray byteArray={byteArray}/>
</main>