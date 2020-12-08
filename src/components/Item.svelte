<script>
  import { Button, Row, Col, Input } from "sveltestrap";
  import { createEventDispatcher } from "svelte";

  export let status;
  export let text;
  export let index;

  const dispatch = createEventDispatcher(); //Callback function

  const removeFromList = (val) => {
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
  <Col class="ml-4 mr-6" md={{ size: 5 }}>
    <Input bind:checked={status} type="checkbox" />
    <span class:checked={status}>{text}</span>
  </Col>
  <Col md={{ size: 2 }}>
    <Button color="danger" outline on:click={() => removeFromList(index)}>
      Delete
    </Button>
  </Col>
  <br />
</Row>
