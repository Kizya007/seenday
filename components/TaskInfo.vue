<template>
  <div class="block info-task">
    <p class="title text-bold">Ссылка для скачивания архива Выгрузки (.zip):</p>
    <div class="block-links">
      <a class="link" :href="'https://seenday.com/' + addres" target="_blank">https://seenday.com/{{ addres }}</a>
      <span class="span-link">скопировать ссылку</span>
    </div>
  </div>
</template>

<script setup>
const props = defineProps({
  addres: {
    type: String,
    default: ""
  }
});

console.log(props);
</script>
