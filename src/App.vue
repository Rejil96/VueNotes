<script setup>
import { ref, onBeforeMount } from "vue";

//This is a third party package from npm which is for creating unique id on every object data
// (In react there is one package which exactly work like this)
import { uuid } from "vue-uuid";
import NoteCard from "./components/NoteCard.vue";

const isShowNoteInputControl = ref(false);
const noteTextData = ref("");
const notesArray = ref([]);
const errorMsg = ref("");

onBeforeMount(() => {
  const getDataFromLS = localStorage.getItem("notes");
  if (getDataFromLS) {
    notesArray.value = JSON.parse(getDataFromLS);
  }
});

// To get random background colors
function getRandomColor() {
  const color = "hsl(" + Math.random() * 360 + ", 100%, 75%)";
  return color;
}

const setDataToLoaclStorage = () => {
  localStorage.setItem("notes", JSON.stringify(notesArray.value));
};

const onAddNote = () => {
  if (noteTextData.value.trim().length < 8) {
    return (errorMsg.value = "* the note should contain atleast 8 charecters!");
  }
  notesArray.value.push({
    id: uuid.v4(),
    noteText: noteTextData.value,
    date: new Date().toLocaleString("en-US"),
    backgroundColor: getRandomColor(notesArray.value),
  });

  setDataToLoaclStorage();

  noteTextData.value = "";
  isShowNoteInputControl.value = false;
};

const deleteFunc = (idDel) => {
  notesArray.value = notesArray.value.filter((eachData) => eachData.id !== idDel);
  setDataToLoaclStorage();
};
</script>

<template>
  <main>
    <div class="overlay" v-if="isShowNoteInputControl">
      <div class="note-input-control-card">
        <p v-if="errorMsg" class="error-text">{{ errorMsg }}</p>
        <textarea
          name=""
          id=""
          cols="30"
          rows="10"
          class="input-control"
          v-model="noteTextData"
        ></textarea>
        <button class="add-note-form-btn" @click="onAddNote()">Add Note</button>
        <button class="close-note-form-btn" @click="isShowNoteInputControl = false">
          Close
        </button>
      </div>
    </div>
    <div class="bg-container">
      <div class="header-container">
        <h1 class="main-heading">Notes</h1>
        <button class="add-note-btn" @click="isShowNoteInputControl = true">+</button>
      </div>

      <div class="notes-listing-container">
        <template v-for="note in notesArray">
          <NoteCard :noteData="note" :deleteFunc="deleteFunc" />
        </template>
      </div>
    </div>
  </main>
</template>

<style scoped>
main {
  width: 100vw;
  min-height: 100vh;
  display: flex;
  box-sizing: border-box;
  margin: 0px;
  padding: 0px;
}

.bg-container {
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding-top: 80px;
}

.header-container {
  width: 50%;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.main-heading {
  font-size: 52px;
  font-weight: bolder;
}

.add-note-btn {
  background-color: #131313;
  width: 70px;
  height: 70px;
  border-radius: 50%;
  color: #ffffff;
  font-weight: bolder;
  font-size: 32px;
  border: none;
  outline: none;
  cursor: pointer;
}

.overlay {
  position: absolute;
  width: 100%;
  height: 100%;
  background-color: rgb(0, 0, 0, 0.57);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 10;
}

.note-input-control-card {
  width: 40%;
  height: 50%;
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: #ffffff;
  padding: 20px;
  z-index: 10;
}

.input-control {
  width: 100%;
  height: 100%;
  font-family: sans-serif;
  font-style: italic;
  padding: 10px;
  font-size: 16px;
  line-height: 24px;
}

.note-input-control-card button {
  border: none;
  cursor: pointer;
  background-color: blueviolet;
  color: #ffffff;
  font-weight: 500;
  height: 60px;
  width: 100%;
  margin: 0px;
  margin-top: 10px;
  font-weight: 600;
  font-size: 18px;
}

.note-input-control-card .close-note-form-btn {
  background-color: #b33434;
}

.notes-listing-container {
  width: 90%;
  height: 100%;
  margin-top: 60px;
  display: flex;
  flex-wrap: wrap;
}

.error-text {
  color: #b33434;
  align-self: flex-start;
}
</style>
