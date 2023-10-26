<template>
  <main class="unload">
    <div class="left-block">
      <CardsUnload />
      <CardsTaskSucces v-for="task in tasks" :task="task" :key="task.id" @getInfo="getInfo" />
    </div>
    <div>
      <Notice />
      <TaskInfo :addres="link" v-if="item" />
    </div>
  </main>
</template>

<script setup>
function getValueAfterColon(inputString) {
  const colonIndex = inputString.indexOf(":");
  if (colonIndex === -1) {
    return null; // Возвращаем null, если двоеточие не найдено
  }

  return inputString.slice(colonIndex + 2).trim();
}

const url = "https://dev-cabinet.seenday.com/e.scripts?page=pages:unload&event=get";

const activeTaskId = ref("");

const link = ref("");

const { data: tasks, execute } = useFetch(url, {
  immediate: false,
  server: false,
  transform: res => {
    const parsedJSON = JSON.parse(res);
    const data = parsedJSON.response.data;

    return data;
  }
});

const urlInfo = `https://dev-cabinet.seenday.com/e.scripts?page=pages:unload&event=get&unload_id=${activeTaskId.value}`;
const { data: item, execute: executeTask } = useFetch(urlInfo, {
  immediate: false,
  server: false,
  transform: res => {
    const parsedJSON = JSON.parse(res);
    const data = parsedJSON.response.data;

    return data;
  }
});

async function getInfo(value) {
  activeTaskId.value = value;
  await executeTask();
  console.log(item,".task");
  link.value = getValueAfterColon(task.value.response.data[0].download_link);
}

async function getTasks() {
  await execute();
}

await getTasks();
</script>

<!-- <script setup>
const linkk = computed(() => (task.value ? task.value.response.data : null));
async function getInfo(valueId) {
  const { data: task } = await useAPIFetch(
    `https://dev-cabinet.seenday.com/e.scripts?page=pages:unload&event=get&unload_id=${valueId}`,
    {
      transform: JSON.parse
    }
  );

  curentTask.value = task.value.response.data[0];

  link.value = getValueAfterColon(task.value.response.data[0].download_link);

  linkk.value = getValueAfterColon(task.value.response.data[0].download_link);



  console.log(valueId, task);
}

console.log(linkk);

const link = ref("");

function getValueAfterColon(inputString) {
  const colonIndex = inputString.indexOf(":");
  if (colonIndex === -1) {
    return null; // Возвращаем null, если двоеточие не найдено
  }

  return inputString.slice(colonIndex + 2).trim();
}

const curentTask = ref({});

const url = "https://dev-cabinet.seenday.com/e.scripts?page=pages:unload&event=get";

const { data: tasks, execute } = useFetch(url, {
  immediate: false,
  transform: res => {
    const parsedJSON = JSON.parse(res);
    const data = parsedJSON.response.data;

    return data;
  }
});

async function getTasks() {
  await execute();
}
await getTasks -->
<!-- </script> -->
