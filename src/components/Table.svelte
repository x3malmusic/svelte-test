<script>
  import TableRow from "./TableRow.svelte";

  export let tasks = [];
  export let changeTask = () => {};
</script>

<div>
  {#each tasks as task}
    <TableRow
      id={task.id}
      name={task.name}
      start={task.start}
      end={task.end}
      {changeTask}
    />
  {/each}
</div>
