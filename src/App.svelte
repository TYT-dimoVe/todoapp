<script>
  import Item from "./components/Item.svelte";
  import { Col, Button, Row, Input, Container, Form } from "sveltestrap";

  let newItem = "";

  let todoList = [
    { text: "Write my first post", status: false },
    { text: "Upload the post to the blog", status: false },
    { text: "Publish the post at Facebook", status: false },
  ];

  let searchTerm = "";

  $: filteredList = todoList.filter(
    (item) => item.text.toLowerCase().indexOf(searchTerm.toLowerCase()) !== -1
  );

  const addToList = () => {
    if (/\S+/.test(newItem)) {
      todoList = [...todoList, { text: newItem, status: false }];
      newItem = "";
    }
  };

  const removeFromList = (event) => {
    todoList.splice(event.detail.index, 1);
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
  hr.dashed {
    border-top: 1px dashed #999;
  }
</style>

<svelte:head>
  <link
    rel="stylesheet"
    href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css" />
</svelte:head>

<Container>
  <Row>
    <Col />
    <Col class="d-flex flex-column sm-12 col-md-8 mt-5">
      <Container class="md-5 col-lg-offset-4">
        <h4>Filter tasks (by name)</h4>
        <Row>
          <Col md={{ size: 6 }}>
            <Input
              bind:value={searchTerm}
              type="text"
              name="textarea"
              id="exampleSearch"
              placeholder="Filter tasks" />
          </Col>
          <Col md={{ size: 2 }}>
            <Button on:click={clearFilter}>Clear</Button>
          </Col>
        </Row>
        <br />
        <h4>TODO</h4>
        {#each filteredList as item, index}
          <Item {...item} {index} on:removeFromList={removeFromList} />
          {#if index !== filteredList.length - 1}
            <Col md={{ size: 7 }}>
              <hr class="dashed" />
            </Col>
          {/if}
        {/each}

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
      </Container>
    </Col>
    <Col />
  </Row>
</Container>
