<script>
  export let status;
  export let title;
  export let index;

  import { Button, Row, Col, Input } from "sveltestrap";
  import { createEventDispatcher } from "svelte";
  const dispatch = createEventDispatcher(); //Callback function

  const removeFromList = () => {
    dispatch("removeFromList", {
      index: index,
    });
  }; 
</script>

<style>
  .checked {
    text-decoration: line-through;
    color: gray;
  }
</style>

<Row class="mt-2 mb-2">
  <Col class="ml-5" md={{ size: 4 }}>
    <Input bind:checked={status} type="checkbox"/>
    <span class:checked={status}>{title}</span>
  </Col>
  <Col class="mr-5" md={{ size: 2 }}>
    {#if status === false }
      <Button color="danger" outline on:click={() => removeFromList(index)}>
        Delete
      </Button>
    {/if}
  </Col>
  <br />
</Row>
