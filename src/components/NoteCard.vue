<template>
  <div class="noteCard">
    <div class="noteHeader">{{ note.title }}</div>
    <div>{{ note.body }}</div>
    <div>Last updated: {{ formatDate(note.updatedAt) }}</div>
    <button @click="editNote">EDIT</button>
    <button @click="deleteNote">DELETE</button>
  </div>
</template>

<script>
export default {
  props: ["note"],
  emits: ["edit-note", "delete-note"],
  methods: {
    editNote() {
      this.$emit("edit-note", this.note.id);
    },
    deleteNote() {
      this.$emit("delete-note", this.note.id);
    },
    formatDate(dateString) {
      const date = new Date(dateString);
      return (
        date.toLocaleDateString("en-US", {
          year: "numeric",
          month: "long",
          day: "numeric",
        }) +
        " at " +
        date.toLocaleTimeString("en-US", { hour: "2-digit", minute: "2-digit" })
      );
    },
  },
};
</script>

<style scoped>
.noteCard {
  background: #eceff1; 
  font-family: "Roboto Mono", monospace;
  border: 2px solid #dfe3e7;
  padding: 15px;
  border-radius: 8px; 
  box-shadow:
    inset 0 0 10px #e6e1e8, 0 2px 4px rgba(0, 0, 0, 0.1);
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  height: 100%;
}

.noteHeader {
  font-family: "Press Start 2P", cursive;
  font-size: medium;
}

#noteTitle {
  font-size: small;
}

.hidden {
  display: none;
}

.noteCard div {
  margin-bottom: 10px; /* Space between the divs and button */
}

.noteCard button {
  align-self: flex-end;
  margin-top: auto; /* Pushes the button to the bottom */
}

button,
.noteCard {
  transition: transform 0.2s, box-shadow 0.2s;
  display: inline-block;
}

.noteCard:hover {
  transform: translateY(-5px);
  box-shadow:
    0 4px 8px rgba(0, 0, 0, 0.2), /* Subtle hover shadow for lift effect */
    inset 0 0 15px #e6e1e8; /* Inner shadow for a pressed effect */
}

.noteContent {
    padding: 10px; /* Padding inside the card for content */
  }

#date {
  font-family: 'Roboto Mono', monospace;
  font-size: small;
}

</style>
