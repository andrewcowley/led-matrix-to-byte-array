<script>
  import { createEventDispatcher } from 'svelte';
  export let grid;

  const dispatch = createEventDispatcher();
  
  function handleClick(msg) {
    dispatch('boxclick', msg)
  }
</script>

<style>
  .panel {
    line-height: 0;
    padding: 1rem;
    background-color: #313131;
  }
  input[type="checkbox"] {
    -webkit-appearance: none;
    appearance: none;
    background-color: #fff;
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
  <div >
    <div class="panel">
      {#each grid as row, i}
        <div>
          {#each row as a, j}
            <input type=checkbox bind:checked={a} on:click={() => handleClick({row:i,box:j})}>
          {/each}
        </div>
      {/each}
    </div>
  </div>
</main>