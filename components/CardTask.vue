<template>
  <main>
    <div @click="getInfo" class="block" :data-status="task.status === 'green' ? 1 : 2">
      <p v-html="task.task_date"></p>
      <p>
        Статус задачи: <span class="text-bold">{{ task.status_text }}</span>
      </p>
      <p>
        ID выгрузки: <span class="text-bold">{{ task.id }}</span>
      </p>
      <p>{{ task.event }}</p>
      <p>
        Размер выгрузки: <span class="text-bold">{{ task.size }}</span>
      </p>
    </div>
  </main>
</template>

<script setup>

const emit = defineEmits(["getInfo"]);

const props = defineProps({
  task: {
    type: Object,
    required: true
  }
});
function getInfo() {
  emit("getInfo",props.task.id)
}

</script>
