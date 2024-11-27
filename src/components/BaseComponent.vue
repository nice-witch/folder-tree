<script setup lang="ts">
import { ref } from "vue";
import ModalComponent from "./ModalComponent.vue";

const isOpenModal = ref(false);

const openModal = () => (isOpenModal.value = true);
const closeModal = () => (isOpenModal.value = false);
const selectFolder = ref<string | null>();

const select = (folder: number) => {
  closeModal();
  selectFolder.value = `Выбранная папка ID: ${folder}`;
};
</script>

<template>
  <button @click="openModal">Открыть</button>
  <p v-if="selectFolder">{{ selectFolder }}</p>

  <ModalComponent
    v-if="isOpenModal"
    title="Дерево папок"
    @select="select"
    @close="closeModal"
  />
</template>
