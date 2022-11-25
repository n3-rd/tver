<script setup>
const props = defineProps({
  imageSrc: String,
});

console.log(props);
</script>
<template>
  <div>
    <div class="show-image w-[22rem] h-[29rem]">
      <!-- {{ props.imageSrc }} -->
      <img class="w-full h-full object-cover" :src="props.imageSrc" />
    </div>
  </div>
</template>
