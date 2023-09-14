<script setup lang="ts">
import { ref } from 'vue';

const showModal = ref(false);

</script>

<template>
  <div v-if="showModal" class="overlay">
    <div class="modal">
      <label for="note">Type your note bellow</label>
      <textarea name="note" id="note" cols="30" rows="10"></textarea>
      <button class="add-note">Add note</button>
      <button @click="showModal = false" class="close-modal">Close</button>
    </div>
  </div>
  <div class="container">
    <header>
      <h1>
        NOTES {{ showModal }}
      </h1>
      <button @click="showModal = true" title="Click here to add a new note">
        +
      </button>
    </header>

    <main>
      <div class="card-container">
        <div class="card">
          <p class="main-text">
            Lorem ipsum dolor sit amet consectetur adipisicing elit. Hic, mollitia saepe dolores odio numquam voluptatibus
            amet minus reprehenderit nihil dicta? Esse at ea voluptatibus non nam, necessitatibus alias provident
            quibusdam.
            Recusandae praesentium odit cum tempora nisi molestiae assumenda porro aliquam vitae aperiam ut quis,
            voluptatem
            impedit libero beatae! Temporibus, ab?
          </p>
          <p class="date">
            14/08/2023
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
  background-color: blueviolet;
  border: 1px solid black;
  border-radius: 16px;
  padding: 1rem;
  margin: 0 1rem 1rem 0;
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
  margin-top: 0.5rem;
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
