<script>
  export let show = false;
  export let item = { id: null, name: "", description: "" };
  export let onSave;
  export let onClose;

  let nameError = "";
  let descError = "";

  function handleSave() {
    nameError = item.name.trim() ? "" : "Name is required.";
    descError = item.description.trim() ? "" : "Description is required.";

    if (nameError || descError) return;

    onSave(item);
    onClose();
  }
</script>

{#if show}
  <div class="modal-overlay" on:click={onClose}>
    <div class="modal" on:click|stopPropagation>
      <h2>{item.id ? "Edit Item" : "Create Item"}</h2>

      <div class="form-group">
        <label for="name">Name</label>
        <input
          id="name"
          type="text"
          bind:value={item.name}
          placeholder="Enter name"
          class="input-field"
        />
        <p class="error">{nameError}</p>
      </div>

      <div class="form-group">
        <label for="description">Description</label>
        <textarea
          id="description"
          bind:value={item.description}
          placeholder="Enter description"
          class="textarea"
        ></textarea>
        <p class="error">{descError}</p>
      </div>

      <div class="modal-actions">
        <button on:click={onClose} class="cancel-btn">Cancel</button>
        <button on:click={handleSave} class="save-btn">
          {item.id ? "Update" : "Create"}
        </button>
      </div>
    </div>
  </div>
{/if}

<style>
  .modal-overlay {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.5);
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .modal {
    background: white;
    padding: 20px;
    border-radius: 10px;
    width: 400px;
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
    text-align: center;
  }

  .modal h2 {
    margin-bottom: 15px;
    font-size: 20px;
  }

  .form-group {
    position: relative;
    width: 100%;
    margin-bottom: 20px;
    text-align: left;
  }

  label {
    display: block;
    font-weight: bold;
    margin-bottom: 5px;
  }

  .input-field,
  .textarea {
    width: 100%;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 5px;
    font-size: 14px;
  }

  .textarea {
    height: 80px;
    resize: none;
  }

  .error {
    color: red;
    font-size: 12px;
    position: absolute;
    bottom: -18px;
    left: 0;
  }

  .modal-actions {
    display: flex;
    justify-content: flex-end;
    gap: 10px;
  }

  .cancel-btn {
    background: #ccc;
    padding: 8px 12px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
  }

  .save-btn {
    background: #007bff;
    color: white;
    padding: 8px 12px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
  }

  .cancel-btn:hover {
    background: #b3b3b3;
  }

  .save-btn:hover {
    background: #0056b3;
  }
</style>
