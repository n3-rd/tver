<script setup>
const props = defineProps({
  title: String,
  years: String,
  summary: String,
  website: String,
  status: String,
  ended: String,
  rating: Number || String || null,
});

console.log(props);
</script>
<template>
  <div>
    <h1 class="text-6xl font-black">{{ props.title }}</h1>
    <div class="show-date font-semibold">
      {{ props.years }} <span v-if="props.ended">- {{ props.ended }}</span>
      <span> ({{ props.status }})</span>
    </div>
    <div
      class="summary py-3"
      v-html="props.summary.slice(0, 600) + '...'"
    ></div>
    <div class="show-rating" v-if="props.rating">
      <span class="font-semibold">Rating: </span>
      {{ props.rating }}
    </div>
    <div class="website py-3">
      <a :href="props.website" target="_blank" class="btn btn-wide">Website</a>
    </div>
  </div>
</template>
