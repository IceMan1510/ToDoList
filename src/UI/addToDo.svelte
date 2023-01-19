<script>
  import Active from "./Blocks/active.svelte";
  import All from "./Blocks/all.svelte";
  import Completed from "./Blocks/completed.svelte";
  import DateBlock from "./Blocks/date.svelte";

  let newToDo = "";
  let block = "";

  //date & time//
  let currentDate = new Date();
  let today = currentDate.getDate();
  let month = currentDate.getMonth() + 1;
  const year = currentDate.getFullYear();
  if (today < 10) today = "0" + today;
  if (month < 10) month = "0" + month;
  let dueDate = year + "-" + month + "-" + today;
  let searchDate = "";
  console.log(searchDate);
  export let todoLists = [];

  const addTodo = () => {
    if (newToDo.trim().length > 0) {
      block = "all";
      let currentTodo = {
        id: todoLists.length + 1,
        title: newToDo,
        completed: false,
        date: dueDate,
      };

      todoLists = [...todoLists, currentTodo];
      todoLists.sort((a, b) => {
        let da = new Date(a.date),
          db = new Date(b.date);
        return da - db;
      });
      console.log(todoLists);
      newToDo = "";
    } else {
      return;
    }
  };

  const removeItem = (index) => {
    todoLists.splice(index, 1);
    todoLists = todoLists;
    console.log("Done");
  };
</script>

<main>
  <div class="container">
    <h2>Just Do It</h2>

    <div class="fixed-bar">
      <input
        class="newToDo"
        placeholder="What Needs To Be Done ? + Enter"
        type="text"
        bind:value={newToDo}
        on:keypress={(e) => {
          if (e.key === "Enter") {
            addTodo();
            newToDo = "";
          }
        }}
      />
      <input type="date" name="" class="date" bind:value={dueDate} />
    </div>

    {#each todoLists as item, i}
      {#if block == "all"}
        <All {item} {removeItem} {i} />
      {:else if block === "active" && item.completed === true}
        <Active {item} {removeItem} {i} />
      {:else if block === "completed" && item.completed === false}
        <Completed {item} {removeItem} {i} />
      {:else if block === "date" && item.date === searchDate}
        <DateBlock {todoLists} {item} {i} />
      {/if}
    {/each}

    {#if todoLists.length > 0}
      <div class="bottom-buttons">
        <button
          on:click={() => {
            block = "all";
          }}>All</button
        >
        <button
          on:click={() => {
            block = "active";
          }}>Completed</button
        >
        <button
          on:click={() => {
            block = "completed";
          }}>Active</button
        >
        <input
          type="date"
          bind:value={searchDate}
          on:change={() => {
            block = "date";
          }}
        />
      </div>
    {/if}
  </div>
</main>

<style>
</style>
