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
    background-color: var(--color-bg-0);
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
    overflow: hidden;
  }

  .content {
    flex: 1;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    gap: 20px;
  }

  .game-content {
    justify-content: flex-start;
    padding-top: 30px;
  }

  .counters {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 20px;
    width: 100%;
  }

  .start-button {
    display: block;
    width: 100%;
    max-width: 300px;
    margin: 20px auto;
    padding: 15px 20px;
    font-size: 1.2rem;
    cursor: pointer;
    background-color: var(--color-theme-1);
    color: var(--color-bg-0);
    border: none;
    transition:
      background-color 0.3s,
      box-shadow 0.3s;
    box-shadow: 0 0 10px rgba(0, 255, 255, 0.5);
  }

  .start-button:hover {
    background-color: var(--color-theme-2);
    box-shadow: 0 0 20px rgba(255, 0, 255, 0.5);
  }

  .back-button {
    position: absolute;
    top: 20px;
    left: 20px;
    background: none;
    border: none;
    color: var(--color-theme-1);
    font-size: 1rem;
    cursor: pointer;
    padding: 5px;
    transition: color 0.3s;
    z-index: 10;
  }

  .back-button:hover {
    color: var(--color-theme-2);
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
    background-color: var(--color-bg-2);
    color: var(--color-text);
    border: 1px solid var(--color-theme-1);
    transition:
      background-color 0.3s,
      box-shadow 0.3s;
  }

  :global(.health-selector button:hover) {
    background-color: var(--color-theme-1);
    color: var(--color-bg-0);
    box-shadow: 0 0 10px rgba(0, 255, 255, 0.5);
  }

  @media (max-width: 600px) {
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
