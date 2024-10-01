<script lang="ts">
  export let initialValue = 100;
  let count = initialValue;

  $: {
    // Reset count when initialValue changes
    count = initialValue;
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
    {count}
  </div>
  <div class="buttons">
    <button class="decrement" on:click={() => decrement(10)}>-10</button>
    <button class="decrement" on:click={() => decrement(1)}>-1</button>
    <button class="increment" on:click={() => increment(1)}>+1</button>
    <button class="increment" on:click={() => increment(10)}>+10</button>
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
    width: 100px;
    height: 100px;
    background-color: #4caf50;
    border-radius: 50%;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 24px;
    color: white;
    cursor: pointer;
    user-select: none;
  }

  .buttons {
    display: flex;
    justify-content: center;
    margin-top: 10px;
  }

  button {
    margin: 0 5px;
    padding: 5px 10px;
    border: none;
    border-radius: 5px;
    color: white;
    cursor: pointer;
  }

  .increment {
    background-color: #2196f3;
  }

  .decrement {
    background-color: #f44336;
  }
</style>
