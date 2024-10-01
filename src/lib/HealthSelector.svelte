<script lang="ts">
  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();
  let selectedHealth = 100;

  const healthOptions = [50, 100, 200];

  function updateHealth(health: number) {
    selectedHealth = health;
    dispatch("healthChange", selectedHealth);
  }
</script>

<div class="health-selector">
  <h2>Select Starting Health</h2>
  <div class="button-group">
    {#each healthOptions as health}
      <button
        class:selected={selectedHealth === health}
        on:click={() => updateHealth(health)}
      >
        {health}
      </button>
    {/each}
  </div>
</div>

<style>
  .health-selector {
    text-align: center;
    margin-bottom: 20px;
  }

  .button-group {
    display: flex;
    justify-content: center;
    gap: 10px;
  }

  button {
    font-size: 16px;
    padding: 5px 15px;
    border: 2px solid #4caf50;
    background-color: white;
    color: #4caf50;
    cursor: pointer;
    border-radius: 5px;
    transition: all 0.3s ease;
  }

  button:hover {
    background-color: #4caf50;
    color: white;
  }

  button.selected {
    background-color: #4caf50;
    color: white;
  }
</style>
