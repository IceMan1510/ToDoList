<script>
  export let item;
  export let removeItem;
  export let i;
</script>

<div class="task">
  <div class="task-wrap">
    <input bind:checked={item.completed} type="checkbox" />
    <span class:checked={item.completed}>{item.title}</span>
  </div>
  <div class="twoItems">
    <span class="dateTag">{item.date}</span>
    <!-- svelte-ignore a11y-click-events-have-key-events -->
    <i class="fa fa-trash fa-2x" on:click={() => removeItem(i)} />
  </div>
</div>
