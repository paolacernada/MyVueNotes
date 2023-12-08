<template>
  <li class="note-item">
    <div v-if="!isEditing">
      <h3 class="note-title">{{ note.title }}</h3>
      <p class="note-body">{{ note.body }}</p>
      <p class="note-updated">{{ updatedAtFormatted }}</p>
      <button @click="deleteNote" class="delete-button">Delete</button>
      <button @click="editNote" class="edit-button">Edit</button>
    </div>
    <div v-else>
      <NoteForm :existingNote="note" @refresh-notes="finishEdit" />
      <button @click="cancelEdit" class="cancel-button">Cancel</button>
    </div>
  </li>
</template>

<script>
import NoteForm from './NoteForm.vue';

export default {
  components: {
    NoteForm,
  },
  props: {
    note: Object,
  },
  data() {
    return {
      isEditing: false
    };
  },
  computed: {
    updatedAtFormatted() {
      const dateOptions = { year: 'numeric', month: 'long', day: 'numeric' };
      const timeOptions = { hour: 'numeric', minute: 'numeric', hour12: true };
      const date = new Date(this.note.updatedAt);
      const formattedDate = date.toLocaleDateString('en-US', dateOptions);
      const formattedTime = date.toLocaleTimeString('en-US', timeOptions);
      return `Last updated: ${formattedDate} at ${formattedTime}`;
    }
  },
  methods: {
    deleteNote() {
      fetch(`http://localhost:3000/notes/${this.note.id}`, {
        method: 'DELETE',
      }).then(() => this.$emit('refresh-notes'));
    },
    editNote() {
      this.isEditing = true;
    },
    cancelEdit() {
      this.isEditing = false;
    },
    finishEdit() {
      this.isEditing = false;
      this.$emit('refresh-notes');
    }
  }
};
</script>

<style scoped>
.note-item {
  background-color: #f9f9f9;
  border: 1px solid #ddd;
  border-radius: 4px;
  padding: 20px;
  margin-bottom: 20px;
}

.note-title {
  font-size: 1.5em;
  margin-bottom: 10px;
  color: #333;
}

.note-body {
  margin-bottom: 10px;
  color: #666;
}

.note-updated {
  color: #999;
  margin-bottom: 15px;
  font-size: 0.85em;
}

.edit-button, .delete-button {
  padding: 5px 10px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  margin-right: 5px;
}

.edit-button {
  background-color: #3498db;
  color: white;
}

.edit-button:hover {
  background-color: #2980b9;
}

.delete-button {
  background-color: #e74c3c;
  color: white;
}

.delete-button:hover {
  background-color: #c0392b;
}

.cancel-button {
  background-color: #f39c12;
  color: white;
}

.cancel-button:hover {
  background-color: #d35400;
}
</style>


