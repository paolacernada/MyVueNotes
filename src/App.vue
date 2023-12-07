<template>

  <div id="noteCardContainer" class="noteCard">
    <div class="windowTitleBar">
      <span class="windowTitle">Note App</span>
      <div class="windowControls"></div>
    </div>
    <div class="noteContent">
      <form @submit.prevent="createNote">
        <input
          type="text"
          v-model="newNote.title"
          placeholder="Title"
          required
        />
        <textarea
          v-model="newNote.body"
          placeholder="Note body"
          required
        ></textarea>
        <button type="submit">Create Note</button>
      </form>

      <h1 class="noteHeader">Vue Notes</h1>

      <div id="container">
        <NoteCard
          v-for="note in notes"
          :key="note.id"
          :note="note"
          @edit-note="displayEditForm"
          @delete-note="deleteNote"
        />
      </div>
    </div>
  </div>
</template>

<script>
import NoteCard from "./components/NoteCard.vue";
import { ref } from "vue";

export default {
  components: {
    NoteCard,
  },
  setup() {
    const notes = ref([]);
    const newNote = ref({ title: "", body: "" });
    const url = "http://localhost:3000/notes/";

    const fetchNotes = async () => {
      const response = await fetch(url);
      notes.value = await response.json();
    };

    const createNote = async () => {
      await fetch(url, {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({
          ...newNote.value,
          updatedAt: new Date().toISOString(),
        }),
      });
      newNote.value = { title: "", body: "" };
      fetchNotes();
    };

    const deleteNote = async (noteId) => {
      await fetch(url + noteId, { method: "DELETE" });
      fetchNotes();
    };

    fetchNotes();

    return { notes, newNote, createNote, deleteNote };
  },
};
</script>

<style scoped>
.noteContent,
#noteCardContainer {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  grid-gap: 20px;
}

form {
  background: #FFFFFF;
  padding: 20px;
  border: 2px solid #B0C4DE;
  border-radius: 8px;
  box-shadow:
    inset 0 0 10px #e6e1e8, /* Inner shadow for a pressed effect */
    0 4px 6px rgba(0, 0, 0, 0.1); /* Drop shadow for depth */
  margin-bottom: 20px;
  width: 50%; 
  margin-left: auto; 
  margin-right: auto; 
}

input[type="text"],
textarea {
  font-family: "Press Start 2P", monospace;
  color: #4a6572;
  width: 100%;
  padding: 10px;
  margin-bottom: 10px;
  background-color: #e6e1e8; 
  border: 1px solid #B0C4DE;
  border-radius: 4px; 
  box-sizing: border-box;
}

input[type="text"]:focus,
textarea:focus {
  outline: none;
  box-shadow: 0 0 5px #637a91; /* Subtle focus glow */
}

textarea {
  resize: vertical;
  height: 100px;
}

button {
  font-family: "Press Start 2P", monospace;
  background-color: #FFD54F; /* Muted button color */
  color: #4a6572;
  border: none;
  padding: 5px 10px;
  margin: 3px;
  text-transform: uppercase;
  cursor: pointer;
  border-radius: 4px; 
  box-shadow:
    0 2px #B0C4DE, /* Bottom border for 3D effect */
    0 4px 6px rgba(0, 0, 0, 0.2); /* Drop shadow for depth */
}

button:hover {
  background-color: #FFCA28; /* Slightly darker yellow on hover */
}

#container {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  grid-gap: 20px;
}

</style>
