<template>
  <main>
    <!-- <MonetoryButton :btnText="'Нажми меня!'" :btnColor="`purple`" /> -->
    <MonetoryInput :value="inputValue" :label="`Название тега`" />
  </main>
</template>

<script setup lang="ts">
// import MonetoryButton from "./components/MonetoryButton.vue";
import MonetoryInput from "./components/MonetoryInput.vue";

const inputValue = "";
</script>
<style>
* {
  box-sizing: border-box;
}
</style>
