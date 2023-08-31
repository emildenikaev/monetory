<template>
  <div class="form-group">
    <label :class="{ 'label-active': inputValue }">{{ label }}</label>
    <input v-model="inputValue" type="text" />
  </div>
</template>

<script setup lang="ts">
import { ref, watch } from "vue";

interface Props {
  value: String;
  label: String;
}

const props = defineProps<Props>();
const inputValue = ref(props.value);

watch(
  () => props.value,
  (newValue) => {
    inputValue.value = newValue;
  }
);
</script>

<style>
.form-group {
  position: relative;
}

label {
  position: absolute;
  top: 14px;
  left: 19px;
  transition: all 0.2s;
  pointer-events: none;
  font-size: 12px;
  line-height: 16px;
  color: #862fde;
}

.label-active {
  transform: translateY(-22px);
  font-size: 12px;
  line-height: 16px;
  color: #862fde;
  padding: 0 4px;
  background-color: #fff;
}

input {
  width: 360px;
  font-size: 14px;
  padding: 14px 17px;
  border: 2px solid #862fde;
  border-radius: 8px;
  color: #16171b;
}

input:focus {
  width: 360px;
  padding: 14px 17px;
  border-color: #862fde;
  border-radius: 8px;
  outline: none;
}
</style>
