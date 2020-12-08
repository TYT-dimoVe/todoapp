<script>
  let newItem = "";

  let todoList = [
    { text: "Write my first post", status: true },
    { text: "Upload the post to the blog", status: false },
    { text: "Publish the post at Facebook", status: false },
  ];

  let searchTerm = "";

  $: filteredList = todoList.filter(
    (item) => item.text.indexOf(searchTerm) !== -1
  );

  const addToList = () => {
    if (/\S+/.test(newItem)) {
      todoList = [...todoList, { text: newItem, status: false }];
      newItem = "";
    }
  };

  const removeFromList = (index) => {
    todoList.splice(index, 1);
    todoList = todoList;
  };

  const handleKeyup = () => {
    if (event.code == "Enter" && /\S+/.test(newItem)) {
      todoList = [...todoList, { text: newItem, status: false }];
      newItem = "";
    }
  };

  const clearFilter = () => {
    searchTerm = "";
  };
</script>

<style>
  .checked {
    text-decoration: line-through;
  }
</style>

<h3>Filter by name</h3>
<input bind:value={searchTerm} />
<button on:click={clearFilter}>Clear</button>

<h3>TODO</h3>
<br />
{#each filteredList as item, index}
  <input bind:checked={item.status} type="checkbox" />
  <span class:checked={item.status}>{item.text}</span>
  <span on:click={() => removeFromList(index)}>❌</span>
  <br />
{/each}

<h3>ADD ITEM</h3>
<input
  bind:value={newItem}
  type="text"
  placeholder="new todo item.."
  on:keyup|preventDefault={handleKeyup} />
<button on:click={addToList}>Add</button>
