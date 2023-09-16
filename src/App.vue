<script setup lang="ts">
import { ref } from 'vue';

type Note = {
  id: number;
  description: string;
  date: Date;
  backgroundColor: string;
}

const showModal = ref(false);
const isNewNote = ref(true);
const newNote = ref("");
const notes = ref<Note[]>([])
const noteIdToEdit = ref(0)

const getRandomColor = () => {
  return "hsl(" + Math.random() * 360 + " 100% 75%)";
}

const addNote = () => {
  notes.value.push({
    id: Math.floor(Math.random() * 1000000),
    description: newNote.value,
    date: new Date(),
    backgroundColor: getRandomColor(),
  })
  showModal.value = false;
  newNote.value = "";
}

const saveNote = () => {
  let note = notes.value[notes.value.findIndex((note) => note.id === noteIdToEdit.value)]
  note.description = newNote.value;
  note.date = new Date();

  showModal.value = false;
  newNote.value = "";
  isNewNote.value = true;
}

const removeNote = (key: number) => {
  notes.value.splice(notes.value.findIndex((note) => { note.id === key }) - 1, 1);
}

const editNote = (key: number) => {
  let note = notes.value[notes.value.findIndex((note) => note.id === key)];
  newNote.value = note.description;
  noteIdToEdit.value = note.id;
  showModal.value = true;
  isNewNote.value = false;
}


</script>

<template>
  <div v-if="showModal" class="overlay">
    <div class="modal">
      <label for="note">Type your note bellow</label>
      <textarea v-model="newNote" name="note" id="note" cols="30" rows="10"></textarea>
      <button v-if="isNewNote" @click="addNote" class="add-note">Add note</button>
      <button v-if="!isNewNote" @click="saveNote" class="add-note">Save note</button>
      <button @click="showModal = false; newNote = ''" class="close-modal">Close</button>
    </div>
  </div>

  <div class="container">
    <header>
      <h1>
        NOTES
      </h1>
      <button @click="showModal = true" title="Click here to add a new note">
        +
      </button>
    </header>

    <main>
      <div class="card-container">
        <div v-for="note in  notes " :key="note.id" :style="{ backgroundColor: note.backgroundColor }" class="card">
          <p class="main-text">
            {{ note.description }}
          </p>
          <p class="date">
            {{ note.date.toLocaleDateString() }}
            <span class="icons-wrapper">
              -
              <button @click="removeNote(note.id)" title="Remove note">
                <i class="uil uil-trash-alt"></i>
              </button>
              <button @click="editNote(note.id)" title="Edit note">
                <i class="uil uil-clipboard-alt"></i>
              </button>
            </span>
          </p>
        </div>
      </div>
    </main>
  </div>
</template>

<style scoped>
header {
  width: 75%;
  height: 25%;
  display: flex;
  align-items: center;
  justify-content: space-between;
  font-size: 32px;
}

header button {
  padding: 8px;
  margin-left: 1.5rem;
  color: white;
  background-color: #2b52dd;
  border: none;
  border-radius: 100%;
  font-size: 24px;
  width: 50px;
  height: 50px;
}

button:hover {
  transform: scale(1.1);
  cursor: pointer;
}

main {
  width: 75%;
  height: 75%;
}

.container {
  width: 100vw;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  background-color: #eff4ff;
}

.card {
  width: 20%;
  height: 40%;
  border: 1px solid black;
  border-radius: 16px;
  padding: 1rem;
  margin: 0 1rem 1rem 0;
}

.card:hover {
  opacity: 0.5;
}

.card:hover .icons-wrapper {
  display: flex;
}

.card-container {
  display: flex;
  align-items: flex-start;
  justify-content: flex-start;
  flex-wrap: wrap;
}

.date {
  width: 100%;
  text-align: right;
  margin-top: 1rem;
  display: flex;
  align-items: flex-end;
  justify-content: flex-end;
  transition: 400ms ease-in-out 0s;
}

.icons-wrapper {
  font-size: 20px;
  display: none;
  transition: 400ms ease-in-out 0s;
}

.icons-wrapper button {
  background-color: transparent;
  border: none;
  font-size: 20px;
}

.icons-wrapper button:hover {
  background-color: transparent;
}

.overlay {
  position: absolute;
  background-color: rgba(0, 0, 0, 0.77);
  width: 100%;
  height: 100%;
  z-index: 10;
  display: flex;
  align-items: center;
  justify-content: center;
}

.modal {
  min-width: 50%;
  height: auto;
  padding: 32px;
  background-color: lightgrey;
  display: flex;
  align-items: center;
  justify-content: space-around;
  flex-direction: column;
  border-radius: 16px;
}

.modal label {
  font-size: 16px;
  margin-bottom: 8px;
}

.modal textarea {
  min-width: 95%;
  border-radius: 16px;
  border: none;
  padding: 16px;
  font-size: 16px;
  margin-bottom: 8px;
}

.modal button {
  width: 100%;
  height: 25px;
  border: none;
  border-radius: 8px;
  margin-bottom: 8px;
  color: white;
}

.modal button:hover {
  transform: scale(1.01);
}

.add-note {
  background-color: #2b52dd;
}

.close-modal {
  background-color: red;
}
</style>
