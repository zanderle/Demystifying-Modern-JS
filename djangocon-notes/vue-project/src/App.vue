<script>
import TalkItem from "./components/TalkItem.vue";

import {} from "./assets/main.css";

export default {
  data() {
    return {
      selectedTalk: null,
      notes: {},
      schedule: null,
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
  mounted() {
    fetch(
      "https://pretalx.evolutio.pt/djangocon-europe-2022/schedule/export/schedule.json"
    )
      .then((resp) => resp.json())
      .then((data) => (this.schedule = data));
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
      if (!this.schedule) return [];
      const { Auditorium: auditorium_talks } =
        this.schedule.schedule.conference.days[0].rooms;
      return auditorium_talks;
    },
  },
};
</script>

<template>
  <ul class="flex-1 h-full overflow-y-scroll" v-if="schedule">
    <template v-for="talk in talks">
      <li v-if="talk.persons.length" :key="talk.id">
        <talk-item :talk="talk" @select="showDetails(talk)"></talk-item>
      </li>
    </template>
  </ul>
  <div v-else class="flex-1">Loading...</div>
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
