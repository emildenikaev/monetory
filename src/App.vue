<template>
  <main>
    <MonetoryModal
      :modalMainText="'Добавление тегов'"
      :modalParagraph="'Вы можете добавить еще'"
      :modalParagraphCount="20"
      :isModalTag="true"
    >
      <template v-slot:input>
        <MonetoryInput
          :value="tagStore.searchInput"
          :label="`Название тега`"
          v-model="tagStore.searchInput"
        />
      </template>

      <template v-slot:button>
        <MonetoryButton
          class="btn-save"
          :btnText="'Сохранить'"
          :btnColor="`purple`"
          @click="saveTagsToLocalStorage"
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
import { useTagStore } from "./stores/TagStore";
import { onMounted } from "vue";

const tagStore = useTagStore();

const saveTagsToLocalStorage = () => {
  const selectedTagsString = JSON.stringify(tagStore.choisenTags);
  localStorage.setItem("selectedTags", selectedTagsString);
};

onMounted(() => {
  const selectedTagsString = localStorage.getItem("selectedTags");
  if (selectedTagsString) {
    tagStore.choisenTags = JSON.parse(selectedTagsString);
  }
});
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
