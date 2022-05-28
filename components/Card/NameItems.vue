<script setup>
// Props
const props = defineProps(["foundNames"]);
// Emits
const emits = defineEmits(["deleteEmit"]);
// Functions
const emitHanlder = (name) => {
  emits("deleteEmit", name);
};
</script>

<template>
  <li class="item" v-for="(name, index) in foundNames" :key="index">
    {{ name }}
    <button @click="emitHanlder(name)" class="delete-button">X</button>
  </li>
</template>
<style scoped>
ul > li {
  position: relative;
  color: white;
  padding: 1rem 2rem;
  border: 1px solid rgb(245, 46, 50);
  background-color: rgb(245, 46, 50);
  border-radius: 10px;
}
button.delete-button {
  position: absolute;
  border: none;
  background: none;
  cursor: pointer;
  right: 0;
  top: 10%;
  color: white;
}
button.delete-button:hover {
  color: #ccc;
}
</style>
