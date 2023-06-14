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
  <main class="h-screen w-screen bg-blue-100">
    <div v-show="showModal" class="fixed inset-0 flex items-center justify-center bg-black bg-opacity-75">
      <div class="w-96 bg-white rounded-lg p-6">
        <textarea v-model.trim="newNoteInput" name="note" id="note" cols="30" rows="10" class="w-full h-32 p-2 text-lg"></textarea>
        <p v-if="errorMessage" class="text-red-500">{{ errorMessage }}</p>
        <button @click="addNote" class="w-full py-2 mt-3 text-white bg-blue-500 rounded-lg">Add Note</button>
        <button class="w-full py-2 mt-3 text-white bg-red-500 rounded-lg" @click="showModal = false">Close</button>
      </div>
    </div>
    <div class="container mx-auto p-10">
      <header class="flex justify-between items-center">
        <h1 class="font-bold text-6xl mb-10">Notes</h1>
        <button @click="showModal = true" class="w-16 h-16 bg-black rounded-full text-white text-4xl flex items-center justify-center">+</button>
      </header>
      <div class="flex flex-wrap -mr-4 -mb-4 p-4">
        <div v-for="note in notes" :key="note.id" class="card mr-4 mb-4 p-2  w-56 max-h-64 overflow-y-auto rounded-md" :style="{ backgroundColor: note.backgroundColor }">
          <p class="main-text whitespace-wrap break-words">{{ note.text }}</p>
          <p class="date">{{ note.date.toLocaleDateString("en-US") }}</p>
        </div>
      </div>
    </div>
  </main>
</template>
