<script setup>
import { ref } from 'vue';

const showModal = ref(false);
const noteMessage = ref('');
const notesArr = ref([]);

const handleModal = () => {
  showModal.value = !showModal.value;
};

const getRandomColor = () => {
  const color = "hsl(" + Math.random() * 360 + ", 100%, 75%)";
  return color;
}

const addNote = () => {
  if (!noteMessage.value) {
    return alert('Please enter a note');
  }

  notesArr.value.push({
    id: Math.floor(Math.random() * 12345),
    text: noteMessage.value,
    date: new Date().toLocaleDateString(),
    color: getRandomColor()
  });
  noteMessage.value = '';
  handleModal();
}

</script>

<template>
  <main>
    <div v-if="showModal" class="overlay">
      <div class="modal">
        <p>x</p>
        <textarea v-model="noteMessage" />
        <button @click="addNote" class="add-btn">Add Note</button>
        <button @click="handleModal" class="close-btn">Close</button>
      </div>
    </div>
    <div class="container">
      <header>
        <h1>Notes</h1>
        <button @click="handleModal">+</button>
      </header>
      <div class="cards-container">
        <div v-for="note in notesArr" class="card" :key="note.id" :style="{ backgroundColor: note.color }">
          <p class=" main-text">{{ note.text }}
          </p>
          <p class="date">{{ note.date }}</p>
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

.card p {
  color: black;

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

.close-btn {
  background-color: red;
}

.modal button {
  padding: 10px 20px;
  font-size: 20px;
  width: 100%;
  border: none;
  color: white;
  cursor: pointer;
  margin-top: 15px;
}

.add-btn {
  background-color: blueviolet;
}

.modal p {
  margin-left: auto;
  font-size: 20px;
  z-index: 100000;
  cursor: pointer;
}

textarea {
  width: 100%;
  height: 200px;
  padding: 5px;
  font-size: 20px;
}
</style>