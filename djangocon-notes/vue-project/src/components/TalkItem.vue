<script>
export default {
  props: {
    talk: { type: Object, required: true },
  },
};
</script>

<template>
  <h2>{{ talk.title }}</h2>
  <h4>{{ talk.speakers }}</h4>
  <p>{{ talk.abstract }}</p>
  <button @click="$emit('select')" class="px-2 py-1 rounded border">
    Show Details
  </button>
  <a :href="talk.url" class="text-blue-400 hover:text-blue-500 mx-4"
    >See talk on pretalx</a
  >
</template>
