<script>
  import Articles from "$lib/components/modals/Articles.svelte";

  let items = [
    {
      id: 1,
      name: "Item 1",
      description: "This is item 1",
      test: "This is item 1",
    },
    { id: 2, name: "Item 2", description: "This is item 2" },
  ];

  let showAddModal = false;
  let showEditModal = false;
  let selectedItem = {};

  function openAddModal() {
    showAddModal = true;
  }

  function openEditModal(item) {
    selectedItem = item;
    showEditModal = true;
  }

  function saveItem(updatedItem) {
    if (updatedItem.id) {
      items = items.map((item) =>
        item.id === updatedItem.id ? updatedItem : item
      );
    } else {
      items = [...items, { ...updatedItem, id: Date.now() }];
    }
    onClose();
  }

  function onClose() {
    showAddModal = false;
    showEditModal = false;
  }
</script>

<div class="container">
  <h1>📋 Items List</h1>

  <button on:click={openAddModal} class="add-btn">➕ Add Item</button>

  <ul class="item-list">
    {#each items as item (item.id)}
      <li class="item">
        <div>
          <h3>{item.name}</h3>
          <p>{item.description}</p>
        </div>
        <button on:click={() => openEditModal(item)} class="edit-btn"
          >✏️ Edit</button
        >
      </li>
    {/each}
  </ul>

  {#if showAddModal}
    <Articles show={showAddModal} onSave={saveItem} {onClose} />
  {/if}
  {#if showEditModal}
    <Articles
      show={showEditModal}
      item={selectedItem}
      onSave={saveItem}
      {onClose}
    />
  {/if}
</div>

<style>
  .container {
    max-width: 600px;
    margin: 40px auto;
    padding: 20px;
    font-family: Arial, sans-serif;
  }

  h1 {
    font-size: 24px;
    margin-bottom: 20px;
  }

  .add-btn {
    background: #28a745;
    color: white;
    padding: 10px 15px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    display: block;
    margin-bottom: 20px;
  }

  .add-btn:hover {
    background: #218838;
  }

  .item-list {
    list-style: none;
    padding: 0;
  }

  .item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 10px;
    background: #f9f9f9;
    border: 1px solid #ddd;
    border-radius: 5px;
    margin-bottom: 10px;
  }

  .item h3 {
    margin: 0;
    font-size: 18px;
  }

  .item p {
    margin: 5px 0 0;
    color: #666;
  }

  .edit-btn {
    background: #007bff;
    color: white;
    padding: 6px 12px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
  }

  .edit-btn:hover {
    background: #0056b3;
  }
</style>
