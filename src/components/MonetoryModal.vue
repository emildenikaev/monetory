<template>
  <div class="modal-wrapper">
    <div class="modal-window">
      <h2>{{ props.modalMainText }}</h2>
      <p>
        {{ props.modalParagraph }} <span>{{ modalParagraphCount }}</span>
      </p>
      <hr />
      <div class="input-container">
        <slot name="input" />
      </div>
      <hr />
      <div class="btn-container">
        <slot name="button" />
      </div>
    </div>
    <div class="overlay"></div>
  </div>
</template>

<script setup lang="ts">
interface Props {
  modalMainText: String;
  modalParagraph: String;
  modalParagraphCount: Number;
}

const props = defineProps<Props>();
</script>

<style scoped lang="scss">
.modal-wrapper {
  position: fixed;
  display: flex;
  width: 100%;
  height: 100%;
  justify-content: center;
  align-items: center;
  background: rgba(0, 0, 0, 0.7);
  z-index: 100;
}

.overlay {
  position: absolute;
  width: 100%;
  height: 100%;
  z-index: 1;
}

.modal-window {
  width: 560px;
  border-radius: 10px;
  background: #fff;
  z-index: 2;
}

h2 {
  color: #16171b;
  line-height: 20px;
  font-size: 16px;
  font-weight: 600;
  margin-top: 40px;
  margin-left: 40px;
}

p {
  line-height: 20px;
  font-size: 14px;
  font-weight: 500;
  color: #8c8f97;
  margin-left: 40px;
  margin-top: 12px;
  margin-bottom: 20px;
}

span {
  line-height: 20px;
  font-size: 16px;
  color: #404144;
}

hr {
  border: 1px solid #ecedf2;
}

.input-container {
  margin-left: 40px;
  margin-top: 40px;
  margin-bottom: 56px;
}

.btn-container {
  margin-left: 40px;
  margin-top: 24px;
  margin-bottom: 24px;
  display: flex;
}

.btn-container:first-child {
  margin-right: 20px;
}
</style>
