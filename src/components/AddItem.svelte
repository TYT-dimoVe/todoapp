<script>
  import { Button, Row, Col, Input } from "sveltestrap";
  import { createEventDispatcher } from "svelte";
  const dispatch = createEventDispatcher(); //Callback function

  let newItem = "";

  const handleKeyup = () => {
    if (event.code == "Enter" && /\S+/.test(newItem)) {
      dispatch("handleKeyup", {
        newItem: newItem,
      });
      newItem = "";
    }
  };

  const addToList = () => {
    if (/\S+/.test(newItem)) {
      dispatch("addToList", {
        newItem: newItem,
      });
      newItem = "";
    }
  };
</script>

<h4>ADD ITEM</h4>
<Row>
  <Col md={{ size: 6 }}>
    <Input
      bind:value={newItem}
      on:keypress={handleKeyup}
      id="addItem"
      type="text"
      placeholder="New todo item.." />
  </Col>
  <Col md={{ size: 2 }}>
    <Button color="primary" on:click={addToList}>Add</Button>
  </Col>
</Row>
