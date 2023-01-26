<script lang="ts">
  import "bootstrap/dist/css/bootstrap.min.css";
  import Square from "./square.svelte";

  const numSquares: number = 8;

  var winCount: number = 0;
  var loseCount: number = 0;

  var squares: number[] = [];
  var numBlue: number = 0;
  var numClicked = 0;

  var started: boolean = false;
  var gameGoing: boolean = true;

  function playButtonClicked() {
    started = true;
    gameGoing = true;
    generateSquares();
  }

  function generateSquares() {
    numClicked = 0;
    numBlue = 0;
    squares = [];
    for (let i = 0; i < numSquares; i++) {
      let val = Math.round(Math.random());
      if (val == 1) {
        numBlue++;
      }
      squares.push(val);
    }
    if (numBlue == 0) {
      generateSquares();
    }
  }

  function handleSquareClicked(event: any) {
    let val = event.detail.val;
    if (val == 0) {
      gameGoing = false;
      loseCount++;
    } else {
      numClicked++;
      if (numClicked == numBlue) {
        gameGoing = false;
        winCount++;
      }
    }
  }
</script>

<div class="row w-100 m-0 p-0 justify-content-center">
  <div class="d-flex justify-content-center"><h1>Click the Blue Ones!</h1></div>
</div>

<div class="row w-100 m-0 p-0 justify-content-center">
  <div class="col-9 d-flex justify-content-center">
      <div class="row w-100 justify-content-center">
          <div class="col-2 d-flex justify-content-center">
            Won: {winCount}
          </div>
          <div class="col-2 d-flex justify-content-center">
            Lost: {loseCount}
        </div>
      </div>
  </div>
</div>

{#if !started}
  <div class="row w-100 m-0 p-0 justify-content-center">
    <div class="d-flex justify-content-center">
      <button on:click={playButtonClicked} class="btn btn-primary">
        Play
      </button>
    </div>
  </div>
{/if}

{#if started}
  <div class="row w-100 m-0 p-0 justify-content-center">
    <div class="col-6 mx-0 px-0">
      <div class="row w-100 mx-0 px-0">
        {#each squares as square}
          <div class="my-3 col-3 d-flex justify-content-center">
            <Square
              on:clicked={handleSquareClicked}
              {gameGoing}
              disabled={!gameGoing}
              val={square}
            />
          </div>
        {/each}
      </div>
    </div>
  </div>
{/if}

{#if started && !gameGoing}
  <div class="row w-100 m-0 p-0 justify-content-center">
    <div class="d-flex justify-content-center">
      <button on:click={playButtonClicked} class="btn btn-primary">
        Play Again
      </button>
    </div>
  </div>
{/if}

<style>
  .page-body {
    background-color: red;
    margin: 0px;
    padding: 0px;
  }
</style>
