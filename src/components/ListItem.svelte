<script>
  import { createEventDispatcher } from "svelte";
  import { Col, Row } from "sveltestrap";
  import Item from "../components/Item.svelte";

  const dispatch = createEventDispatcher(); //Callback function

  export let filteredList;

  const removeFromList = (event) => {
    dispatch("removeFromList", {
      index: event.detail.index,
    });
  };

  const handleChange = (event) => {
    dispatch("handleChange", {
      index: event.detail.index,
      status: event.detail.status,
    });
  }
</script>

<style>
  hr.dashed {
    border-top: 1px dashed #999;
  }
</style>

<h4>TODO</h4>
{#each filteredList as item, index}
  <Item {...item} {index} on:removeFromList={removeFromList} on:handleChange={handleChange}/>
  {#if index !== filteredList.length - 1}
    <Col md={{ size: 7 }}>
      <hr class="dashed" />
    </Col>
  {/if}
{/each}
<Row class="mb-4" />
