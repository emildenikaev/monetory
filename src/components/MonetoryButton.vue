<template>
  <div>
    <button
      class="btn"
      :class="[
        props.btnColor === 'purple' && 'btn-purple',
        props.btnColor === 'gray' && 'btn-gray',
      ]"
    >
      {{ props.btnText }}
    </button>
  </div>
</template>

<script setup lang="ts">
enum btnColor {
  purple = "purple",
  gray = "gray",
}

interface Props {
  btnText: String;
  btnColor: btnColor;
}

const props = defineProps<Props>();
</script>

<style style="scoped" lang="scss">
.btn {
  cursor: pointer;
  border-radius: 10px;
  size: 14px;
  line-height: 16px;
  padding: 8px 16px;

  &:hover {
    opacity: 0.8;
  }

  &-purple {
    border: 2px solid #862fde;
    color: #fff;
    background-color: #862fde;
  }

  &-gray {
    border: 2px solid #f6f6f9;
    color: #16171b;
    background-color: #f6f6f9;
  }
}
</style>
