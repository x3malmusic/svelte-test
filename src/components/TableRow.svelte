<script>
  export let id = "";
  export let changeTask = () => {};
  export let name = "";
  export let start = "";
  export let end = "";

  function changeData() {
    const task = {
      id,
      name,
      start,
      end,
      progress: 0,
    };
    changeTask(task);
  }
</script>

<div class="table-row">
  <input type="text" on:input={changeData} bind:value={name} />
  <input type="date" on:change={changeData} bind:value={start} />
  <input type="date" on:change={changeData} bind:value={end} />
</div>

<style>
  .table-row {
    display: flex;
    gap: 8px;
  }
</style>
