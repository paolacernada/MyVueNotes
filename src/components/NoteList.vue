<template>
    <div>
      <NoteForm @refresh-notes="fetchNotes" />
      <ul>
        <NoteItem
          v-for="note in notes"
          :key="note.id"
          :note="note"
          @refresh-notes="fetchNotes"
        />
      </ul>
    </div>
  </template>
  
  <script>
  import NoteForm from './NoteForm.vue'
  import NoteItem from './NoteItem.vue'
  
  export default {
    components: {
      NoteForm,
      NoteItem
    },
    data() {
      return {
        notes: []
      }
    },
    methods: {
      fetchNotes() {
        fetch('http://localhost:3000/notes/')
          .then(response => response.json())
          .then(data => this.notes = data)
      }
    },
    mounted() {
      this.fetchNotes()
    }
  }
  </script>
  