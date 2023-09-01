<template>
  <div class="modal-wrapper">
    <div class="modal-window">
      <h2>{{ props.modalMainText }}</h2>
      <p>
        {{ props.modalParagraph }}
        <span>{{ +modalParagraphCount - tagStore.choisenTags.length }}</span>
      </p>
      <hr />
      <div
        class="input-container"
        :class="
          (tagStore.searchInput.length > 1 ||
            tagStore.choisenTags.length > 0) &&
          isModalTag &&
          'isModalTag'
        "
      >
        <slot name="input" />
        <ul
          v-if="
            tagStore.searchInput &&
            tagStore.searchInput.length > 1 &&
            isModalTag &&
            tagStore.filteredTagNames.length > 0
          "
          class="list"
        >
          <li
            v-for="tag in tagStore.filteredTagNames"
            :key="tag"
            class="tag"
            @click="addToChoisenTags(tag)"
          >
            {{ tag }}
          </li>
        </ul>
        <div
          v-if="
            tagStore.searchInput &&
            tagStore.searchInput.length > 1 &&
            isModalTag &&
            tagStore.filteredTagNames.length === 0
          "
          class="no-tag"
        >
          По запросу ничего не найдено
        </div>
        <hr
          v-if="
            tagStore.searchInput &&
            tagStore.searchInput.length > 1 &&
            tagStore.choisenTags.length > 0
          "
        />
        <ul v-if="tagStore.choisenTags.length > 0" class="list">
          <li
            v-for="choisenTag in tagStore.choisenTags"
            :key="choisenTag"
            class="tag"
            @click="deleteFromChoisenTags(choisenTag)"
          >
            {{ choisenTag }}
            <img
              src="../assets/iconClose.svg"
              alt="Значок закрытия"
              class="close"
            />
          </li>
        </ul>
      </div>
      <hr />
      <div class="btn-container">
        <slot name="button" />
      </div>
    </div>
    <div class="overlay" @click="closeModalOnOutsideClick"></div>
  </div>
</template>

<script setup lang="ts">
import { useTagStore } from "../stores/TagStore";

interface Props {
  modalMainText: String;
  modalParagraph: String;
  modalParagraphCount: Number;
  isModalTag: Boolean;
}

const props = defineProps<Props>();

const tagStore = useTagStore();

const addToChoisenTags = (tag: string) => {
  if (tagStore.choisenTags.length < 20 && !tagStore.choisenTags.includes(tag)) {
    tagStore.choisenTags.push(tag);
  }
};

const deleteFromChoisenTags = (tag: string) => {
  const index = tagStore.choisenTags.indexOf(tag);
  if (index > -1) {
    tagStore.choisenTags.splice(index, 1);
    const selectedTagsString = JSON.stringify(tagStore.choisenTags);
    localStorage.setItem("selectedTags", selectedTagsString);
  }
};

const closeModalOnOutsideClick = (event: MouseEvent) => {
  if (
    event.target instanceof HTMLElement &&
    !event.target.closest(".modal-window")
  ) {
    tagStore.isModalOpen = false;
  }
};
</script>

<style scoped lang="scss">
.modal-wrapper {
  display: flex;
  position: fixed;
  width: 100vw;
  min-height: 100%;
  justify-content: center;
  align-items: center;
  background: rgba(0, 0, 0, 0.7);
  z-index: 100;
  top: 0;
  left: 0;
}

.overlay {
  position: absolute;
  width: 100%;
  min-height: 100%;
  z-index: 1;
}

.modal-window {
  width: 560px;
  border-radius: 10px;
  background: #fff;
  z-index: 2;
  margin-top: 40px;
  margin-bottom: 40px;
}

h2 {
  color: #16171b;
  line-height: 20px;
  font-size: 16px;
  font-weight: 600;
  margin-top: 40px;
  margin-left: 41px;
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

.isModalTag {
  margin-bottom: 24px;
}

.no-tag {
  color: #8c8f97;
  font-weight: 500;
  font-size: 14px;
  line-height: 20px;
  margin-top: 20px;
  margin-bottom: 24px;
}

.tag {
  padding: 8px 12px 8px 12px;
  border-radius: 4px;
  background: #f6f6f9;
  margin: 8px;
  color: #404144;
  font-size: 14px;
  line-height: 16px;
  cursor: pointer;
  margin-left: 0;

  &:hover {
    opacity: 0.8;
  }
}

.list {
  display: flex;
  flex-wrap: wrap;
  list-style: none;
  padding-left: 0;
  padding-right: 100px;
  max-height: 140px;
  overflow: auto;
}

.close {
  width: 10px;
  height: 10px;
  margin-left: 8px;
}
</style>
