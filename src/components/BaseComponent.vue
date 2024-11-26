<script setup lang="ts">
import { ref } from "vue";
import ModalComponent from "./ModalComponent.vue";

const isOpenModal = ref(false);

const openModal = () => (isOpenModal.value = true);
const closeModal = () => (isOpenModal.value = false);
const selectFolder = ref<string | null>();

const select = (folder: string) => {
  closeModal();
  selectFolder.value = folder;
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

<style scoped></style>
