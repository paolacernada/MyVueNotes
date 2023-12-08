<template>
  <div id="app" class="container">
    <AppHeader />
    <NoteList />
  </div>
</template>

<script>
import AppHeader from './components/Header.vue';
import NoteList from './components/NoteList.vue'

export default {
  components: {
    AppHeader,
    NoteList, 
  },
};
</script>

<style>

.container {
  max-width: 800px;
  margin: 0 auto;
  padding: 40px 20px;
  background: #f5f5f5; 
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1); 
  border-radius: 8px; 
}

button {
  background-color: #3498db;
  border: none;
  border-radius: 4px;
  color: white;
  padding: 10px 20px;
  text-transform: uppercase;
  letter-spacing: 1px;
  cursor: pointer;
}

button:hover {
  background-color: #2980b9;
}

input, textarea {
  width: 300px;
  padding: 10px;
  margin: 10px 0;
  border: 1px solid #ddd;
  border-radius: 4px;
  box-sizing: border-box;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  margin: 10px 0;
  padding: 10px;
  background-color: #ecf0f1;
  border-radius: 4px;
}
</style>

