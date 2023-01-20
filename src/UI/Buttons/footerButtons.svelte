<script>
  export let searchDate;

  import { createEventDispatcher } from "svelte";
  const dispatch = createEventDispatcher();
</script>

<div class="bottom-buttons">
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
    type="date"
    bind:value={searchDate}
    on:change={() => {
      dispatch("message", { block: "date", searchDate: searchDate });
    }}
  />
</div>
