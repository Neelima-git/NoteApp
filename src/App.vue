<script setup>
import { ref } from "vue";

// Reactive variables
const showModal = ref(false); // Indicates whether the modal is visible or not
const newNoteInput = ref(""); // Input field for new note
const errorMessage = ref(""); // Error message to display
const notes = ref([]); // Array of notes

// Generates a random HSL color
const getRandomColor = () => {
  return "hsl(" + Math.random() * 360 + ", 100%, 75%)";
};

// Adds a new note to the notes array
const addNote = () => {
  if (!newNoteInput.value.length) {
    return (errorMessage.value = "Note can't be empty!"); // Display error message if the note is empty
  }
  notes.value.push({
    id: Math.floor(Math.random() * 1000000), // Generates a random ID for the note
    text: newNoteInput.value, // The content of the note
    date: new Date(), // Current date and time
    backgroundColor: getRandomColor(), // Random background color for the note
  });
  showModal.value = false; // Close the modal after adding the note
  newNoteInput.value = ""; // Clear the input field
  errorMessage.value = ""; // Clear the error message
};
</script>

<template>
  <main>
    <div v-show="showModal" class="overlay">
      <div class="modal">
        <textarea
          v-model.trim="newNoteInput"
          name="note"
          id="note"
          cols="30"
          rows="10"
        ></textarea>
        <p v-if="errorMessage">{{ errorMessage }}</p>
        <button @click="addNote">Add Note</button>
        <button class="close" @click="showModal = false">Close</button>
      </div>
    </div>
    <div class="container">
      <header>
        <h1>Notes</h1>
        <button @click="showModal = true">+</button>
      </header>
      <div class="cards-container">
        <div
          v-for="note in notes"
          :key="note.id"
          class="card"
          :style="{ backgroundColor: note.backgroundColor }"
        >
          <p class="main-text">{{ note.text }}</p>
          <p class="date">{{ note.date.toLocaleDateString("en-US") }}</p>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped>
.container {
    max-width: 1000px;
    padding: 10px;
    margin: 0 auto
  }

  h1 {
    font-weight: bold;
    margin-bottom: 25px;
    font-size: 75px;
  }

  .card {
    width: 225px;
    height: 225px;
    background-color: rgb(237, 182, 44);
    padding: 10px;
    border-radius: 15px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    margin-right: 20px;
    margin-bottom: 20px;
  }

  .card:hover {
    cursor: pointer;
    opacity: 0.9;
  }

  .main-text {
    line-height: 1.25;
    font-size: 17.5px;
    font-weight: bold;
  }

  .date {
    font-size: 12.5px;
    margin-top: auto;
  }

  header {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  header button {
    border: none;
    padding: 10px;
    width: 50px;
    height: 50px;
    cursor: pointer;
    background-color: rgb(21, 20, 20);
    border-radius: 1000px;
    color: white;
    font-size: 20px;
  }
  .cards-container {
    display: flex;
    flex-wrap: wrap;
  }

  .overlay {
    position: absolute;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.77);
    transform: translate(-50%, -50%);
    top: 50%;
    left: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    z-index: 10;
  }

  main {
    height: 100vh;
    width: 100vw;
  }
  .modal {
    width: 750px;
    background-color: white;
    border-radius: 10px;
    padding: 30px;
    position: relative;
    display: flex;
    flex-direction: column;
  }

  .modal button {
    padding: 10px 20px;
    font-size: 20px;
    width: 100%;
    background-color: blueviolet;
    border: none;
    color: white;
    cursor: pointer;
    margin-top: 15px;

  }

  textarea {
    width: 100%;
    height: 200px;
    padding: 5px;
    font-size: 20px;
  }
.modal .close {
  background-color: rgb(193, 15, 15);
  margin-top: 7px;
}
.modal p{
  color: red;
}
</style>
