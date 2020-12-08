<script>
  export let status;
  export let text;
</script>

<style>
  .checked {
    text-decoration: line-through;
  }
</style>

<input bind:checked={status} type="checkbox" />
<span class:checked={status}>{text}</span>
<button>Delete</button>
