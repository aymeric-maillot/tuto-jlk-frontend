<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';

const persons = ref([]);

const fetchPersons = async () => {
  try {
    const response = await axios.get('http://localhost:8080/api/persons');
    persons.value = response.data;
  } catch (error) {
    console.error('There was an error fetching the persons:', error);
  }
};

onMounted(() => {
  fetchPersons();
});
</script>

<template>
  <div>
    <p>Hello la famille !</p>
    <v-text-field label="Label"></v-text-field>
    <ul>
      <li v-for="person in persons" :key="person.id">
        {{ person.name }} - {{ person.email }}
      </li>
    </ul>
  </div>
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}

.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}

.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
