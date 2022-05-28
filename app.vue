<script setup>
import names from "@/data.js";
const userSelection = ref({
  gender: "Boy",
  popularity: "Trendy",
  length: "Long",
});
const foundNames = ref([]);
const changeHanlder = (newValue, prop) => {
  userSelection.value[`${prop}`] = newValue;
};

const displaySelection = () => {
  foundNames.value = [];
  const filteredNames = names.filter((name, index) => {
    if (
      name.gender === userSelection.value.gender &&
      name.popularity === userSelection.value.popularity &&
      name.length === userSelection.value.length
    ) {
      return name;
    }
  });
  if (filteredNames.length > 0) {
    foundNames.value = filteredNames.map((name) => {
      return name.name;
    });
  }

  console.log("founde result", foundNames.value);
};
const removeName = (shouldDeleteName) => {
  foundNames.value = foundNames.value.filter((name) => {
    return name !== shouldDeleteName;
  });
  console.log("found names", foundNames.value);
};
const optionsArray = [
  {
    title: "1) Choose a gender ",
    category: "gender",
    buttons: ["Boy", "Girl"],
  },
  {
    title: "2) Choose name popularity ",
    category: "popularity",
    buttons: ["Trendy", "Unique"],
  },
  {
    title: "3) Choose name's length ",
    category: "length",
    buttons: ["All", "Short", "Long"],
  },
];
</script>

<template>
  <div class="container">
    <h1 class="text-title">Baby Name Generator</h1>
    <p>Choose your options and click the "Find names" button below</p>
    <div class="options-container">
      <Options
        v-for="option in optionsArray"
        :key="option.title"
        :options="option"
        :user-choice="userSelection"
        @submitEmit="changeHanlder"
      />
    </div>
    <div class="options-submit__container">
      <button @click="displaySelection" class="primary">Find Names</button>
    </div>
  </div>
  <CardName @sendEmit="removeName" :found-names="foundNames" />
</template>

<style scoped>
div.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin: 2rem auto;
  max-width: 700px;
  font-family: Arial, Helvetica, sans-serif;
  box-shadow: 0 0 10px 0px #ccc;
  padding: 1.5rem;
}
div.options-container,
div.option-container {
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-items: center;
}
div.options-container h4 {
  font-size: 1.5rem;
  color: rgb(249, 87, 89);
}
.text-title {
  font-weight: bold;
  font-family: inherit;
  font-size: 2rem;
}

div.options-submit__container {
  padding: 2rem;
}
button.primary {
  background-color: rgb(249, 87, 89);
  color: white;
  cursor: pointer;
  border-radius: 12px;
  padding: 0.75rem 2rem;
  border: none;
}
button.primary:hover {
  box-shadow: 0 0 5px 0 rgb(243, 106, 108);
}
</style>
