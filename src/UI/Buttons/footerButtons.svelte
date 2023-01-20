<script>
  import { fade, fly, slide, scale } from "svelte/transition";
  export let searchDate;
  import { createEventDispatcher } from "svelte";
  const dispatch = createEventDispatcher();
</script>

<div class="bottom-buttons" transition:fly={{ x: 0, y: 200 }}>
  <button
    on:click={() => {
      dispatch("message", { block: "all" });
    }}>All</button
  >
  <button
    on:click={() => {
      dispatch("message", { block: "active" });
    }}>Completed</button
  >
  <button
    on:click={() => {
      dispatch("message", { block: "completed" });
    }}>Active</button
  >
  <input
    type="text"
    placeholder="Search By Date"
    onfocus="(this.type = `date`)"
    bind:value={searchDate}
    on:change={() => {
      dispatch("message", { block: "date", searchDate: searchDate });
    }}
  />
</div>
