<script setup>
import {
  ref
} from "vue";
const showModal = ref(false);
const newNote = ref("trying That");
const notes = ref([]);
const empty=ref(false);

const addNote = () => {

  if(note.value.length==0){
    empty.value=true;
    return;
  }
  else{
    empty.value=false;
  }
  notes.value.push({
    id: Math.floor(Math.random() * 1000000),
    text: newNote.value,
    date: new Date(),
    backgroundColor: getRandomColor(),
  })
  showModal.value = false;
  newNote.value = "";
}

function getRandomColor() {
  return "hsl(" + Math.random() * 360 + ", 100%, 75%)";
}
</script>

<template>
  <main>

    <div v-if="showModal" class="overlay">
      <div class="modal">
        <textarea v-model.trim="newNote" name="note" id="note" cols="30" rows="10"></textarea>
        <div v-if="empty" class="error">Cant enter empty note</div>
        <button @click="addNote">Add Note</button>
        <button class="close" @click="showModal = false , empty=false">Close</button>
      </div>
    </div>

    <div class="container">
      <header>
        <h1>Notes</h1>
        <button @click="showModal = true"> + </button>
      </header>
      <div class="cards-container">
        <div v-for="note in notes" 
        v-bind:key="note.id"
        class="card"
        :style="{ backgroundColor: note.backgroundColor }">
          <p class="main-text">{{ note.text }}</p>
          <p class="date">{{ note.date.toLocaleDateString("en-US") }}</p>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped>
main {
  height: 100vh;
  width: 100vw;
  background-color: #FFF1DC;

}

.container {
  max-width: 1000px;
  padding: 10px;
  margin: 0 auto;
}

header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

h1 {
  font-weight: bold;
  margin-bottom: 25px;
  font-size: 75px;
}

header button {
  border: none;
  padding: 10px;
  width: 50px;
  height: 50px;
  cursor: pointer;
  background-color: rgb(21, 20, 20);
  border-radius: 100%;
  color: white;
  font-size: 25px;
}

.card {
  width: 10vw;
  height: 20vh;
  background: rgb(240, 240, 74);
  border-radius: 15px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  margin-right: 20px;
  margin-bottom: 20px;
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
  z-index: 10;
  display: flex;
  align-items: center;
  justify-content: center;
}

.modal {
  width: 750px;
  background-color: white;
  border-radius: 10px;
  padding: 30px;
  position: relative;
  display: relative;
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
  margin: top 15px;
  ;
}

.main-text {
  text-align: center;

}

.date {
  margin-left: 10px;
}

#note {
  width: 100%;
}

.modal .close {
  background-color: rgb(190, 16, 16);
  margin-top: 10px;
}

.modal .error{
  color: rgb(190, 16, 16);
  font-size: 2vh;
  text-align: center;
}
</style>
