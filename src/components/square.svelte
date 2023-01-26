<script lang="ts">
  import "bootstrap/dist/css/bootstrap.min.css";
  import { createEventDispatcher } from "svelte";
  const clicked = createEventDispatcher();

  export let val: number;
  export let disabled: boolean;
  export let gameGoing: boolean;

  $: resetClicked(gameGoing);

  let hasBeenClicked: boolean = false;

  function handleClick() {
    if (!disabled) {
      if (!hasBeenClicked) {
        clicked("clicked", { val: val });
      }
      hasBeenClicked = true;
    }
  }

  function resetClicked(going: boolean){
      //console.log(dis);
    if(going){
        hasBeenClicked = false;
    }
  }
</script>

<div
  on:click={handleClick}
  class="square {val === 0
    ? hasBeenClicked
      ? 'black'
      : 'red'
    : hasBeenClicked
    ? 'green'
    : 'blue'}"
/>

<style>
  .square {
    width: 50px;
    height: 50px;
  }
  .blue {
    background-color: blue;
  }
  .red {
    background-color: red;
  }
  .green {
    background-color: lightgreen;
  }
  .black {
    background-color: black;
  }
</style>
