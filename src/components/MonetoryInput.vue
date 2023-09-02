<template>
  <div class="form-group">
    <label :class="{ 'label-active': modelValue }">{{ label }}</label>
    <input v-model="modelValue" @input="updateValue" type="text" />
  </div>
</template>

<script setup lang="ts">
import { ref, watch } from "vue";

interface Props {
  modelValue: String;
  label: String;
}

const props = defineProps<Props>();

const emit = defineEmits<{
  (e: "update:modelValue", value: String): void;
}>();

const modelValue = ref<String>(props.modelValue);

watch(modelValue, (newValue) => {
  emit("update:modelValue", newValue);
});

function updateValue(event: Event) {
  const target = event.target as HTMLInputElement;
  modelValue.value = target.value;
  emit("update:modelValue", modelValue.value);
}
</script>

<style lang="scss">
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
  font-weight: 500;
  color: #862fde;
}

.label-active {
  transform: translateY(-22px);
  font-size: 12px;
  line-height: 16px;
  color: #862fde;
  padding: 0 4px;
  font-weight: 500;
  background-color: #fff;
}

input {
  width: 360px;
  font-size: 14px;
  padding: 14px 17px;
  border: 2px solid #862fde;
  border-radius: 8px;
  color: #16171b;
  font-weight: 500;

  &:focus {
    width: 360px;
    padding: 14px 17px;
    border-color: #862fde;
    border-radius: 8px;
    outline: none;
  }
}
</style>
