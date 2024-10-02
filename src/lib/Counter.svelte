<script lang="ts">
  import { fade, scale } from "svelte/transition";
  import { cubicOut } from "svelte/easing";

  export let initialValue = 100;
  let count = initialValue;
  let prevCount = count;
  let direction: "up" | "down" | null = null;

  $: {
    direction = count < prevCount ? "down" : count > prevCount ? "up" : null;
    prevCount = count;
  }

  function increment(amount: number) {
    count += amount;
  }

  function decrement(amount: number) {
    count -= amount;
  }

  function reset() {
    count = initialValue;
  }

  function handleDoubleTap() {
    let lastTap = 0;
    return () => {
      const now = new Date().getTime();
      const timesince = now - lastTap;
      if (timesince < 300 && timesince > 0) {
        reset();
      }
      lastTap = now;
    };
  }
</script>

<div class="counter-container">
  <div class="counter" on:click={handleDoubleTap()}>
    <div class="counter-value">
      {#key count}
        <span
          in:scale={{
            start: 0.8,
            opacity: 0,
            duration: 300,
            easing: cubicOut,
          }}
          out:fade={{ duration: 200 }}
        >
          {count}
        </span>
      {/key}
    </div>
  </div>
  <div class="buttons">
    <div class="button-row">
      <button class="increment" on:click={() => increment(1)}>+1</button>
      <button class="increment" on:click={() => increment(5)}>+5</button>
      <button class="increment" on:click={() => increment(10)}>+10</button>
    </div>
    <div class="button-row">
      <button class="decrement" on:click={() => decrement(1)}>-1</button>
      <button class="decrement" on:click={() => decrement(5)}>-5</button>
      <button class="decrement" on:click={() => decrement(10)}>-10</button>
    </div>
  </div>
</div>

<style>
  .counter-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin: 20px;
  }

  .counter {
    width: 120px;
    height: 120px;
    background-color: var(--color-bg-2);
    border: 2px solid var(--color-theme-1);
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 28px;
    color: var(--color-theme-1);
    cursor: pointer;
    user-select: none;
    position: relative;
    overflow: hidden;
  }

  .counter::before {
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
  }

  .counter-value {
    background-color: var(--color-bg-2);
    width: 94%;
    height: 94%;
    display: flex;
    justify-content: center;
    align-items: center;
    position: relative;
    z-index: 1;
  }

  .counter-value span {
    display: inline-block;
    text-shadow: 0 0 10px var(--color-theme-1);
  }

  .buttons {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-top: 15px;
  }

  .button-row {
    display: flex;
    justify-content: center;
    margin-bottom: 10px;
  }

  button {
    margin: 0 5px;
    padding: 12px 18px;
    border: none;
    background-color: var(--color-bg-2);
    color: var(--color-text);
    cursor: pointer;
    transition: all 0.3s ease;
    border: 1px solid var(--color-theme-1);
    font-size: 1.125rem;
  }

  button:hover {
    background-color: var(--color-theme-1);
    color: var(--color-bg-0);
    box-shadow: 0 0 10px var(--color-theme-1);
  }

  .increment {
    border-color: var(--color-theme-1);
  }

  .decrement {
    border-color: var(--color-theme-2);
  }

  .increment:hover {
    background-color: var(--color-theme-1);
    box-shadow: 0 0 10px var(--color-theme-1);
  }

  .decrement:hover {
    background-color: var(--color-theme-2);
    box-shadow: 0 0 10px var(--color-theme-2);
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
    .counter {
      width: 100px;
      height: 100px;
      font-size: 24px;
    }

    button {
      padding: 9px 15px;
      font-size: 1.05rem;
    }

    .button-row {
      margin-bottom: 5px;
    }
  }
</style>
