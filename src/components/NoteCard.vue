<script setup>
const { noteData, deleteFunc } = defineProps(["noteData", "deleteFunc"]);

const onDeleteClicked = () => {
  deleteFunc(noteData.id);
};
</script>

<template>
  <div class="note-card" :style="{ backgroundColor: noteData.backgroundColor }">
    <p class="note-text-data">{{ noteData.noteText }}</p>
    <div class="note-card-footer" :style="{ backgroundColor: noteData.backgroundColor }">
      <p class="note-text-date">{{ noteData.date }}</p>
      <button class="delete-note-btn" @click="onDeleteClicked">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          width="16"
          height="16"
          fill="currentColor"
          class="bi bi-trash3-fill"
          viewBox="0 0 16 16"
        >
          <path
            d="M11 1.5v1h3.5a.5.5 0 0 1 0 1h-.538l-.853 10.66A2 2 0 0 1 11.115 16h-6.23a2 2 0 0 1-1.994-1.84L2.038 3.5H1.5a.5.5 0 0 1 0-1H5v-1A1.5 1.5 0 0 1 6.5 0h3A1.5 1.5 0 0 1 11 1.5Zm-5 0v1h4v-1a.5.5 0 0 0-.5-.5h-3a.5.5 0 0 0-.5.5ZM4.5 5.029l.5 8.5a.5.5 0 1 0 .998-.06l-.5-8.5a.5.5 0 1 0-.998.06Zm6.53-.528a.5.5 0 0 0-.528.47l-.5 8.5a.5.5 0 0 0 .998.058l.5-8.5a.5.5 0 0 0-.47-.528ZM8 4.5a.5.5 0 0 0-.5.5v8.5a.5.5 0 0 0 1 0V5a.5.5 0 0 0-.5-.5Z"
          />
        </svg>
      </button>
    </div>
  </div>
</template>

<style scoped>
.note-card {
  width: 300px;
  height: 250px;
  margin-right: 20px;
  margin-bottom: 20px;
  padding: 10px 10px 0px 10px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  box-shadow: 1px 0px 21px -6px rgba(0, 0, 0, 0.75);
  overflow-y: auto;
  position: relative;
  z-index: 1;
}

.note-text-data {
  line-height: 24px;
  font-size: 18px;
  word-wrap: break-word;
}

.note-text-date {
  align-self: flex-end;
}

.delete-note-btn {
  background-color: transparent;
  border: none;
  cursor: pointer;
  width: 40px;
  height: 40px;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: black;
  color: #ffffff;
  border-radius: 50%;
  margin-right: 10px;
}

.note-card-footer {
  display: flex;
  align-items: center;
  justify-content: space-between;
  position: sticky;
  bottom: 0px;
  padding: 10px;
}
</style>
