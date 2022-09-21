<script>
import schedule from "./assets/schedule";
import TalkItem from "./components/TalkItem.vue";

import {} from "./assets/main.css";

export default {
  data() {
    return {
      selectedTalk: null,
      notes: {},
    };
  },
  components: {
    TalkItem,
  },
  methods: {
    showDetails(talk) {
      this.selectedTalk = talk;
    },
  },
  computed: {
    talks() {
      const talks = this.auditorium_talks.map((t) => {
        t.speakers = t.persons.map((p) => p.public_name).join(", ");
        return t;
      });
      return talks;
    },
    auditorium_talks() {
      const { Auditorium: auditorium_talks } =
        schedule.schedule.conference.days[0].rooms;
      return auditorium_talks;
    },
  },
};
</script>

<template>
  <ul class="flex-1 h-full overflow-y-scroll">
    <template v-for="talk in talks">
      <li v-if="talk.persons.length" :key="talk.id">
        <talk-item :talk="talk" @select="showDetails(talk)"></talk-item>
      </li>
    </template>
  </ul>
  <div class="flex-1 h-full overflow-y-scroll px-4">
    <span class="font-bold"
      >Notes taken: {{ Object.keys(notes).length }} / {{ talks.length }}</span
    >
    <template v-if="selectedTalk">
      <h2>{{ selectedTalk.title }}</h2>
      <h4>{{ selectedTalk.speakers }}</h4>
      <p>{{ selectedTalk.description }}</p>
      <textarea
        :name="`notes-{selectedTalk.id}`"
        :id="`notes-{selectedTalk.id}`"
        rows="10"
        class="w-full"
        v-model="notes[selectedTalk.id]"
      ></textarea>
    </template>
  </div>
</template>

<style></style>
