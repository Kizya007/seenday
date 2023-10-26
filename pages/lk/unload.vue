<template>
  <main class="unload">
    <div class="left-block">
      <CardsInfo />
      <CardTask v-for="task in tasks" :task="task" :key="task.id" @getInfo="getInfo" />
    </div>
    <div class="right-block">
      <Notice />
      <TaskInfo v-if="showInfo" :downloadLink="downloadLink" @close="close" />
    </div>
  </main>
</template>

<script setup>
const urlTasks = "https://dev-cabinet.seenday.com/e.scripts?page=pages:unload&event=get";

const downloadLink = ref("");

const showInfo = ref(false);

function close() {
  showInfo.value = false
}

const { data: tasks, execute } = useAPIFetch(urlTasks, {
  immediate: false,
  transform: res => {
    const parsedJSON = JSON.parse(res);
    const data = parsedJSON.response.data;

    return data;
  }
});

async function getInfo(idTask) {
  const urlTasks = `https://dev-cabinet.seenday.com/e.scripts?page=pages:unload&event=get&unload_id=${idTask}`;
  const { data: task, execute: executeTask } = useAPIFetch(urlTasks, {
    immediate: false,
    transform: res => {
      const parsedJSON = JSON.parse(res);
      const data = parsedJSON.response.data[0];

      return data;
    }
  });

  await executeTask();
  downloadLink.value = task.value.download_link;
  showInfo.value = true
}

async function getTasks() {
  await execute();
}

await getTasks();
</script>
