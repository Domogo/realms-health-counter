<script lang="ts">
  export let initialValue: number;
  let count = initialValue;

  function increment() {
    count += 1;
  }

  function decrement() {
    count -= 1;
  }
</script>

<div class="counter">
  <button class="decrement" on:click={decrement}>-</button>
  <span class="count">{count}</span>
  <button class="increment" on:click={increment}>+</button>
</div>

<style>
  .counter {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 10px;
  }

  button {
    font-size: 1.5rem;
    width: 60px;
    height: 60px;
    border: none;
    border-radius: 50%;
    background-color: #4caf50;
    color: white;
    cursor: pointer;
    transition: background-color 0.3s;
  }

  button:hover {
    background-color: #45a049;
  }

  .count {
    font-size: 2rem;
    min-width: 80px;
    text-align: center;
  }
</style>
