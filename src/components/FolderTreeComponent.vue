<script setup lang="ts">
import { ref, watch } from "vue";

interface Folder {
  id: number;
  name: string;
  children: Folder[];
}
interface Props {
  folders: Folder[];
}
const props = defineProps<Props>();

const emit = defineEmits<{
  (e: "chooseFolder", folder: number): void;
}>();

const handleFolderClick = (folderId: number) => {
  emit("chooseFolder", folderId);
};
</script>

<template>
  <div v-for="folder in folders" :key="folder.id" class="details">
    <details v-if="folder.children.length">
      <summary @click="handleFolderClick(folder.id)">
        {{ folder.name }}
      </summary>
      <FolderTreeComponent
        :folders="folder.children"
        @chooseFolder="handleFolderClick"
      />
    </details>
    <p v-else @click="handleFolderClick(folder.id)">
      {{ folder.name }}
    </p>
  </div>
</template>

<style scoped>
.details {
  padding-left: 15px;
}
</style>
