<script>
  import { Col, Container, Row } from "sveltestrap";
  import AddItem from "./components/AddItem.svelte";
  import Filter from "./components/Filter.svelte";
  import ListItem from "./components/ListItem.svelte";

  let searchTerm = "";
  let todoList = [
    { title: "Write my first post", status: false },
    { title: "Write my second post", status: false },
    { title: "Write my third post", status: false },
  ];

  $: filteredList = todoList.filter(
    (item) => item.title.toLowerCase().indexOf(searchTerm.toLowerCase()) !== -1
  );

  const addToList = (event) => {
    todoList = [...todoList, { title: event.detail.newItem, status: false }];
  };

  const removeFromList = (event) => {
    todoList.splice(event.detail.index, 1);
    todoList = todoList;
  };
</script>

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
        <Filter bind:searchTerm />
        <ListItem bind:filteredList on:removeFromList={removeFromList} />
        <AddItem on:handleKeyup={addToList} on:addToList={addToList} />
      </Container>
    </Col>
    <Col />
  </Row>
</Container>
