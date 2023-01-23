<script>
  import { fade, fly, slide, scale } from "svelte/transition";
  export let item;
  export let removeItem;
  export let i;
  var countDownDate = new Date(`${item.date} 24:00:00`).getTime();
  var now;
  var timeLeft;
  var days = 0;
  var hours = 0;
  var timeFunc = setInterval(function () {
    now = new Date().getTime();
    timeLeft = countDownDate - now;
    days = Math.floor(timeLeft / (1000 * 60 * 60 * 24));
    hours = Math.floor((timeLeft % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
    console.log(days);
  }, 1000);
  timeFunc;
</script>

<div class="task" transition:fly={{ x: 200, y: 0 }}>
  <div class="task-wrap">
    <input bind:checked={item.completed} type="checkbox" />
    <span class:checked={item.completed}>{item.title}</span>
  </div>
  <div class="twoItems">
    {#if days < 0 || hours < 0}
      <span style="color:red;">Time Up</span>
    {:else if days > "1"}
      <span>{days} Days</span>
    {:else}
      <span style="color:red;">{hours} Hrs</span>
    {/if}
    <span class="dateTag">{item.date}</span>
    <!-- svelte-ignore a11y-click-events-have-key-events -->
    <i class="fa fa-trash fa-2x" on:click={() => removeItem(i)} />
  </div>
</div>
