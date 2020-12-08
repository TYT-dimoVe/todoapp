<script>
  import { Button, Row, Col, Input } from "sveltestrap";
  export let searchTerm = "";

  const clearFilter = () => {
    searchTerm = "";
  };

  const handleKeyup = (e) => {
    if (e.keyCode === 27) {
      searchTerm = "";
    }
  };
</script>

<h5>Filter tasks (by name)</h5>
<Row class="mb-4">
  <Col md={{ size: 6 }}>
    <Input
      bind:value={searchTerm}
      on:keypress={handleKeyup}
      type="text"
      name="textarea"
      id="exampleSearch"
      placeholder="Filter tasks" />
  </Col>
  <Col md={{ size: 2 }}>
    <Button on:click={clearFilter}>Clear</Button>
  </Col>
  <Row />
</Row>
