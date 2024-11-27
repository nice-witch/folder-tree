<script setup lang="ts">
import { ref } from "vue";
import FolderTreeComponent from "./FolderTreeComponent.vue";
import { mockFolders } from "@/mockData";

interface Props {
  title: string;
}
const props = defineProps<Props>();

const emit = defineEmits<{
  (e: "close"): void;
  (e: "select", folder: number): void;
}>();

const selectFolder = ref<number>(0);

const chooseFolder = (folder: number) => {
  selectFolder.value = folder;
};
</script>

<template>
  <Teleport to="body">
    <div class="overlay">
      <div class="modal-container">
        <h2>{{ title }}</h2>
        <div class="folder-container">
          <FolderTreeComponent
            :folders="mockFolders"
            @chooseFolder="chooseFolder"
          />
        </div>
        <div class="button-container">
          <button
            :disabled="!selectFolder"
            @click="$emit('select', selectFolder)"
          >
            Ок
          </button>
          <button @click="$emit('close')">Закрыть</button>
        </div>
      </div>
    </div>
  </Teleport>
</template>

<style scoped>
.overlay {
  position: fixed;
  top: 0;
  left: 0;
  display: flex;
  justify-content: center;
  width: 100vw;
  height: 100vh;
  background: #00000080;
}

.modal-container {
  display: flex;
  flex-direction: column;
  gap: 20px;
  align-self: center;
  width: 390px;
  padding: 20px;
  border-radius: 15px;
  background-color: #eee;
}

.button-container {
  display: flex;
  justify-content: space-between;
}
</style>
