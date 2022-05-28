<script setup>
const props = defineProps({
  foundNames: {
    type: Array,
  },
});
const emit = defineEmits(["sendEmit"]);
const SubmitEmit = (name) => {
  console.log("received name");
  emit("sendEmit", name);
};
</script>

<template>
  <div class="card-container">
    <ul class="foundNames-items" v-if="foundNames.length > 0">
      <CardNameItems @deleteEmit="SubmitEmit" :found-names="foundNames" />
    </ul>
    <div v-else>
      <h2>Not found names</h2>
    </div>
  </div>
</template>

<style scoped>
div.card-container {
  max-width: 500px;
  padding: 1.2rem;
  display: flex;
  margin: 1rem auto;
  flex-direction: row;
  justify-content: center;
}
div.card-container > ul {
  position: relative;
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: space-between;
  width: 100%;
}
</style>
