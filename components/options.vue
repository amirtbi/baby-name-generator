<script setup>
// props
const props = defineProps({
  options: {
    type: Object,
    require: true,
  },
  userChoice: {
    type: Object,
    required: true,
  },
});
// Emits
const emits = defineEmits(["submitEmit"]);
const emitHanlder = (event, prop) => {
  const selectedItem = event.target.textContent;
  const propertyValue = prop;
  emits("submitEmit", selectedItem, propertyValue);
};
</script>

<template>
  <div class="option-container">
    <h4>{{ options.title }}</h4>
    <div class="options-buttons">
      <button
        v-for="(btn, index) in options.buttons"
        :key="index"
        :class="userChoice[`${options.category}`] === btn && 'option-active'"
        @click="emitHanlder($event, options.category)"
      >
        {{ btn }}
      </button>
    </div>
  </div>
</template>

<style scoped>
div.option-container {
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-items: center;
}
div.options-buttons {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  width: 50%;
}
div.options-buttons button {
  border: none;
  padding: 0.75rem 2rem;
  background-color: white;
  outline: 1px solid rgb(249, 87, 89);

  color: rgb(249, 87, 89);
  cursor: pointer;

  font-weight: bold;
  font-size: 1rem;
}
button.btn-right {
  border-top-right-radius: 15px;
  border-bottom-right-radius: 15px;
}
button.btn-left {
  border-top-left-radius: 15px;
  border-bottom-left-radius: 15px;
}

button.option-active {
  background-color: rgb(249, 87, 89) !important;
  color: white !important;
}
div.options-buttons > button:first-of-type {
  border-top-left-radius: 12px;
  border-bottom-left-radius: 12px;
}
div.options-buttons > button:last-of-type {
  border-top-right-radius: 12px;
  border-bottom-right-radius: 12px;
}
</style>
