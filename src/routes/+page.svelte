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
      <button on:click={startGame}>Start Game</button>
    </div>
  {:else}
    <div class="content">
      <div class="counters">
        <Counter initialValue={startingHealth} />
        <Counter initialValue={startingHealth} />
      </div>
      <button on:click={goBack}>Back to Health Selection</button>
    </div>
  {/if}
</div>

<style>
  :global(body, html) {
    margin: 0;
    padding: 0;
    height: 100%;
  }

  .container {
    display: flex;
    flex-direction: column;
    min-height: 100vh;
    max-width: 800px;
    margin: 0 auto;
    padding: 20px;
    box-sizing: border-box;
  }

  .content {
    flex: 1;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
  }

  h1 {
    text-align: center;
    font-size: 2rem;
    margin-bottom: 20px;
  }

  .counters {
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
    gap: 20px;
    flex: 1;
    align-items: center;
  }

  button {
    display: block;
    width: 100%;
    max-width: 300px;
    margin: 20px auto;
    padding: 15px 20px;
    font-size: 1rem;
    cursor: pointer;
    background-color: #4caf50;
    color: white;
    border: none;
    border-radius: 5px;
    transition: background-color 0.3s;
  }

  button:hover {
    background-color: #45a049;
  }

  @media (max-width: 600px) {
    h1 {
      font-size: 1.5rem;
    }

    .counters {
      flex-direction: column;
    }

    button {
      font-size: 0.9rem;
      padding: 12px 15px;
    }
  }
</style>
