<script lang="ts">
  import Counter from "$lib/Counter.svelte";
  import HealthSelector from "$lib/HealthSelector.svelte";

  let startingHealth = 100;
  let gameStarted = false;

  function handleHealthChange(event: CustomEvent<number>) {
    startingHealth = event.detail;
  }

  function startGame() {
    gameStarted = true;
  }

  function goBack() {
    gameStarted = false;
  }
</script>

<svelte:head>
  <meta name="viewport" content="width=device-width, initial-scale=1" />
</svelte:head>

<div class="container">
  {#if !gameStarted}
    <div class="content">
      <HealthSelector on:healthChange={handleHealthChange} />
      <button class="start-button" on:click={startGame}>Start Game</button>
    </div>
  {:else}
    <button class="back-button" on:click={goBack}>← Back</button>
    <div class="content game-content">
      <div class="counters">
        <Counter initialValue={startingHealth} />
        <Counter initialValue={startingHealth} />
      </div>
    </div>
  {/if}
</div>

<style>
  :global(body, html) {
    margin: 0;
    padding: 0;
    height: 100%;
    overflow: hidden;
  }

  .container {
    display: flex;
    flex-direction: column;
    height: 100vh;
    max-width: 800px;
    margin: 0 auto;
    padding: 20px;
    box-sizing: border-box;
    position: relative;
  }

  .content {
    flex: 1;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    gap: 20px;
    overflow: auto;
  }

  .game-content {
    justify-content: flex-start;
    padding-top: 60px;
  }

  .counters {
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
    gap: 20px;
    width: 100%;
    max-height: calc(100vh - 100px);
    overflow: auto;
  }

  .start-button {
    display: block;
    width: 100%;
    max-width: 300px;
    margin: 20px auto;
    padding: 15px 20px;
    font-size: 1.2rem;
    cursor: pointer;
    background-color: #4caf50;
    color: white;
    border: none;
    border-radius: 5px;
    transition: background-color 0.3s;
  }

  .start-button:hover {
    background-color: #45a049;
  }

  .back-button {
    position: absolute;
    top: 20px;
    left: 20px;
    background: none;
    border: none;
    color: #4caf50;
    font-size: 1rem;
    cursor: pointer;
    padding: 5px;
    transition: color 0.3s;
    z-index: 10;
  }

  .back-button:hover {
    color: #45a049;
    text-decoration: underline;
  }

  :global(.health-selector) {
    display: flex;
    flex-direction: column;
    gap: 15px;
    width: 100%;
    max-width: 300px;
  }

  :global(.health-selector button) {
    font-size: 1.5rem;
    padding: 20px;
    margin: 0;
  }

  @media (max-width: 600px) {
    .counters {
      flex-direction: column;
      align-items: center;
    }

    .start-button {
      font-size: 1rem;
      padding: 15px;
    }

    :global(.health-selector button) {
      font-size: 1.2rem;
      padding: 15px;
    }
  }
</style>
