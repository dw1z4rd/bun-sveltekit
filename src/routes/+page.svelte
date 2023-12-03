<!-- @format -->
<script lang="ts">
  import { onDestroy } from "svelte";
  import { count, decrement, increment } from "../stores";

  let countVal: number;

  const unsubscribe = count.subscribe((val) => {
    countVal = val;
  });

  onDestroy(unsubscribe);

  $: isNeg = countVal < 0 ? true : false;
  $: isZero = countVal === 0 ? true : false;
  $: isPos = countVal > 0 ? true : false;
</script>

<div class="w-1/2 mx-auto block p-6">
  <h1
    class:text-red-700={isNeg}
    class:text-slate-700={isZero}
    class:text-emerald-700={isPos}
    class="text-8xl font-bold text-center"
  >
    {countVal}
  </h1>
</div>
<div class="w-full block p-8">
  <button
    class="p-2 rounded-xl bg-emerald-700 text-white w-28 float-left"
    on:click={decrement}>-</button
  >
  <button
    class="p-2 rounded-xl bg-emerald-700 text-white w-28 float-right"
    on:click={increment}>+</button
  >
</div>
