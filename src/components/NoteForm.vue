<template>
  <form class="note-form" @submit.prevent="handleSubmit">
    <input type="text" v-model="note.title" placeholder="Title" class="note-input" required/>
    <textarea v-model="note.body" placeholder="Body" class="note-textarea" required></textarea>
    <button type="submit" class="note-button">
      {{ isEditing ? 'Update Note' : 'Add Note' }}
    </button>
  </form>
</template>

<script>
export default {
  props: {
    existingNote: {
      type: Object,
      default: () => ({ title: '', body: '', id: null })
    }
  },
  data() {
    return {
      note: { ...this.existingNote },
      isEditing: this.existingNote.id !== null
    };
  },
  methods: {
    handleSubmit() {
      const method = this.isEditing ? 'PATCH' : 'POST';
      const url = `http://localhost:3000/notes/${this.isEditing ? this.note.id : ''}`;
      
      fetch(url, {
        method: method,
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ ...this.note, updatedAt: new Date().toISOString() })
      })
      .then(() => {
        this.$emit('refresh-notes');
        if (!this.isEditing) {
          this.note.title = '';
          this.note.body = '';
          this.isEditing = false;
        }
      });
    }
  }
};
</script>

<style scoped>

form {
  margin: 20px auto;
  padding: 20px;
  background-color: #fff;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  max-width: 500px;
}

.note-form {
  background: #fff;
  padding: 30px;
  border-radius: 8px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  margin-bottom: 30px;
}

.note-input, .note-textarea {
  width: 100%;
  padding: 8px;
  margin-bottom: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

input:focus, textarea:focus {
  outline: none;
  border-color: #3498db;
  box-shadow: 0 0 4px rgba(52, 152, 219, 0.6);
}

button {
  width: 100%;
  padding: 10px;
  border-radius: 4px;
  border: none;
  background-color: #3498db;
  color: white;
  cursor: pointer;
  transition: background-color 0.3s;
}

button:hover {
  background-color: #2980b9;
}

button:active {
  background-color: #2471a3;
}

</style>


