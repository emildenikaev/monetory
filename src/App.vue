<template>
  <main>
    <!-- <MonetoryButton :btnText="'Нажми меня!'" :btnColor="`purple`" /> -->
    <MonetoryModal
      :modalMainText="'Добавление тегов'"
      :modalParagraph="'Вы можете добавить еще'"
      :modalParagraphCount="20"
    >
      <template v-slot:input>
        <MonetoryInput :value="inputValue" :label="`Название тега`" />
      </template>
      <template v-slot:button>
        <MonetoryButton
          class="btn-save"
          :btnText="'Сохранить'"
          :btnColor="`purple`"
        />
        <MonetoryButton :btnText="'Отмена'" :btnColor="`gray`" />
      </template>
    </MonetoryModal>
  </main>
</template>

<script setup lang="ts">
import MonetoryButton from "./components/MonetoryButton.vue";
import MonetoryInput from "./components/MonetoryInput.vue";
import MonetoryModal from "./components/MonetoryModal.vue";

const inputValue = "";
</script>
<style>
@import url("https://fonts.cdnfonts.com/css/montserrat");

* {
  box-sizing: border-box;
  font-family: "Montserrat", sans-serif;
}

.btn-save {
  margin-right: 20px;
}
</style>
