<script setup>
  import { ref } from "vue";

  const showModal = ref(false);
  const newNote = ref("");
  const notes = ref([]);

  function getRandomColor () {
    return "hsl(" + Math.floor(Math.random() * 360) + ", 100%, 75%";
  }

  function createNote() {
    if(newNote.value.length == 0) {
      return showModal.value = false;
    }
    notes.value.push({
      id: Math.floor(Math.random() * 1000000),
      text: newNote.value,
      date: new Date(),
      backgroundColor: getRandomColor(),  
    });
    showModal.value = false;
    newNote.value = '';
  }
</script>

<template>

  <div v-if="showModal" class="overlay">
    <div class="modal">
      <textarea v-model.trim="newNote" name="note" id="note"></textarea>
      <div class="control">
        <button id="add" @click="createNote">Add note</button>
        <button id="rem" @click="showModal = false">Cancel</button>
      </div>
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
        :style="{ backgroundColor: note.backgroundColor}">
        <p class="main-text">{{ note.text }}</p>
        <p class="date">{{ note.date.toLocaleDateString() }}</p>
      </div>
    </div>
  </div>

</template>

<style scoped>
header, .cards-container, .overlay, .control {
  display: flex;
  align-items: center;
}
.container {
  max-width: 1000px;
  padding: 10px;
  margin: 0 auto;
}

header {
  justify-content: space-between;
  margin-bottom: 25px;
}

h1 {
  font-size: 70px;
  font-weight: bold;
  color: rgba(0, 0, 0, .9);
}

header button {
  border: none;
  padding: 5px;
  width: 50px;
  height: 50px;
  cursor: pointer;
  background-color: rgba(0, 0, 0, .9);
  border-radius: 50%;
  color: white;
  font-size: xx-large;
  font-weight: bold;
}
.cards-container {
  justify-content: flex-start;
  flex-wrap: wrap;
  gap: 20px;
}
.card{
  width: 225px;
  height: 225px;
  background-color: rgb(237, 182, 44);
  padding: 10px;
  border-radius: 15px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  color: black;
}
.date {
  font-size: 13px;
  font-weight: bold;
}

.overlay {
  position: absolute;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, .7);
  justify-content: center;
}
.modal {
  width: 100%;
  text-align: center;
}

textarea {
  resize: none;
  width: 80%;
  height: 200px;
  margin: 0 auto 15px;
  padding: 10px;
  border: 1.5px solid black;
  border-radius: 10px;
  outline: none;
  font-size: 16px;
  overflow: hidden;
}
.control {
  width: 80%;
  margin: auto;
  justify-content: center;
  gap: 50px;
}

#add, #rem {
  padding: 8px;
  border-radius: 5px;
  font-weight: bold;
  border: none;
  cursor: pointer;
  box-shadow: 1px 1px 5px black,
              -1px -1px 5px black;
  font-size: 15px;
  color: white;
  min-width: 82px;
}

#add {
  background-color: blue;
}

#rem {
  background-color: red;
}

@media (max-width: 700px) {
  .cards-container {
    justify-content: center;
  }
  .card{
    width: 280px;
    height: 280px;
  }
}
</style>
