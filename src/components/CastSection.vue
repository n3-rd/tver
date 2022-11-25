<script setup>
const props = defineProps({
  cast: Array,
});

console.log(props);
</script>
<template>
  <div class="text-[3rem] font-semibold py-8 pl-8">Cast</div>

  <div class="w-full grid grid-cols-5 gap-4">
    <div v-for="person in props.cast" :key="person.person.id" class="w-33">
      <div class="text-center">
        <img
          :src="person.person.image.medium"
          class="rounded-full w-32 h-32 mb-4 mx-auto object-cover"
          alt="Avatar"
        />
        <h5 class="text-xl font-medium leading-tight mb-2">
          {{ person.person.name }}
        </h5>
      </div>
    </div>
  </div>
</template>
