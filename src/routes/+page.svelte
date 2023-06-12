<script>
  import Gantt from "frappe-gantt";
  import { onMount } from "svelte";
  import Table from "../components/Table.svelte";

  let gantt;
  $: tasks = [
    {
      id: Date.now().toString(),
      name: "test",
      start: startDate,
      end: endDate,
      progress: 0,
    },
  ];

  let taskName = "";
  let startDate = "2023-06-12";
  let endDate = "2023-06-13";

  onMount(() => {
    gantt = new Gantt("#gantt", tasks, {
      on_date_change: function (task) {
        const changedTask = {
          ...task,
          start: new Date(task._start + " UTC").toISOString().split("T")[0],
          end: task._end.toISOString().split("T")[0],
        };
        changeTask(changedTask);
      },
    });
  });

  function addTask() {
    tasks = [
      ...tasks,
      {
        id: Date.now().toString(),
        name: taskName,
        start: startDate,
        end: endDate,
        progress: 0,
      },
    ];
    gantt.refresh(tasks);
  }

  function changeTask(task) {
    tasks = tasks.map((t) => {
      if (task.id === t.id) return task;
      return t;
    });
    gantt.refresh(tasks);
  }
</script>

<div class="container">
  <div class="chart">
    <Table {tasks} {changeTask} />
  </div>
  <div id="gantt" />
</div>

<div class="inputs">
  <input bind:value={taskName} type="text" placeholder="task name" />
  <input bind:value={startDate} type="date" placeholder="start date" />
  <input bind:value={endDate} type="date" placeholder="end date" />
</div>

<button on:click={addTask}>add task</button>

<style>
  .container {
    display: flex;
    width: 100%;
  }
  .chart {
    width: 50%;
  }
  #gantt {
    width: 50%;
  }
  .inputs {
    display: flex;
    gap: 8px;
    margin-bottom: 8px;
  }
</style>
