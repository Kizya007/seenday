<template>
  <div class="block info-task">
    <p class="title text-bold">Ссылка для скачивания архива Выгрузки (.zip):</p>
    <div class="block-links">
      <a class="link" :href="downloadLink" target="_blank">{{ downloadLink }}</a>
      <span class="span-link" @click="copyLinkToClipboard(downloadLink)">скопировать ссылку</span>
    </div>
    <button @click="close" class="btn-close">Закрыть</button>
  </div>
</template>

<script setup>
import { defineProps } from "vue";

const emit = defineEmits(["close"]);

const props = defineProps({
  task: {
    type: Object,
    required: true
  },
  downloadLink: {
    type: String,
    default: ""
  }
});
async function copyLinkToClipboard(copyValue) {
  try {
    await navigator.clipboard.writeText(copyValue);
  } catch (error) {
    console.error("Error copying link to clipboard:", error);
  }
}
function close() {
  emit("close");
}

console.log(props);
</script>
