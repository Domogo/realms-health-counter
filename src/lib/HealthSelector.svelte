<script lang="ts">
  import { createEventDispatcher } from "svelte";
  import { fade, scale } from "svelte/transition";
  import { cubicOut } from "svelte/easing";

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
        {#key health}
          <span
            in:scale={{
              start: 0.8,
              opacity: 0,
              duration: 300,
              easing: cubicOut,
            }}
            out:fade={{ duration: 200 }}
          >
            {health}
          </span>
        {/key}
      </button>
    {/each}
  </div>
</div>

<style>
  .health-selector {
    text-align: center;
    margin-bottom: 20px;
  }

  h2 {
    color: var(--color-theme-1);
    text-shadow: 0 0 10px var(--color-theme-1);
    margin-bottom: 15px;
  }

  .button-group {
    display: flex;
    justify-content: center;
    gap: 15px;
  }

  button {
    width: 80px;
    height: 80px;
    font-size: 20px;
    padding: 10px;
    border: 2px solid var(--color-theme-1);
    background-color: var(--color-bg-2);
    color: var(--color-text);
    cursor: pointer;
    transition: all 0.3s ease;
    position: relative;
    overflow: hidden;
  }

  button::before {
    content: "";
    position: absolute;
    top: -50%;
    left: -50%;
    width: 200%;
    height: 200%;
    background: conic-gradient(
      from 0deg,
      transparent,
      var(--color-theme-1),
      transparent 360deg
    );
    animation: rotate 4s linear infinite;
    opacity: 0;
    transition: opacity 0.3s ease;
  }

  button:hover::before,
  button.selected::before {
    opacity: 1;
  }

  button span {
    position: relative;
    z-index: 1;
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100%;
    height: 100%;
    background-color: var(--color-bg-2);
  }

  button:hover span,
  button.selected span {
    color: var(--color-theme-1);
    text-shadow: 0 0 10px var(--color-theme-1);
  }

  button.selected {
    box-shadow: 0 0 15px var(--color-theme-1);
  }

  @keyframes rotate {
    0% {
      transform: rotate(0deg);
    }
    100% {
      transform: rotate(360deg);
    }
  }

  @media (max-width: 600px) {
    button {
      width: 70px;
      height: 70px;
      font-size: 18px;
    }
  }
</style>
