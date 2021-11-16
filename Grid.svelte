<script>
  import converter from "hex2dec";
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
    console.log(hexadecimalNumber);
    return `0x${hexadecimalNumber}`;
  });
</script>

<style>
  .panel {
    line-height: 0;
    padding: 1rem;
    background-color: #313131;
  }
  input[type="checkbox"] {
    /* Add if not using autoprefixer */
    -webkit-appearance: none;
    appearance: none;
    /* For iOS < 15 to remove gradient background */
    background-color: #fff;
    /* Not removed via appearance */
    margin: 0 0.1rem 0.1rem 0;
    font: inherit;
    color: currentColor;
    width: 1.2rem;
    height: 1.2rem;
    border: 1px solid currentColor;
    border-radius: 50%;
    transform: translateY(-0.075em);
  }

  input[type="checkbox"]:last-of-type {
    margin-right: 0;
  }

  input[type="checkbox"]:checked {
    background-color: red;
  }
</style>
<main>
<!-- checkboxes -->
<div class="panel">
  {#each grid as g}
    <div>
      {#each g as a}
        <input type=checkbox bind:checked={a}>
      {/each}
    </div>
  {/each}
</div>

<!-- values -->
<!-- <div>
  {#each grid as g}
    <div>
      {#each g as a}
        {+a}
      {/each}
    </div>
  {/each}
</div> -->

<!-- hexidecimal values -->
<h2>Byte array</h2>
<div>
{byteArray}
</div>

</main>