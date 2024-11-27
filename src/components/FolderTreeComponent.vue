<script setup lang="ts">
import { ref } from "vue";

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

const chooseFolder = ref<number>();

const handleFolderClick = (folderId: number) => {
  chooseFolder.value = folderId;
  emit("chooseFolder", folderId);
};
</script>

<template>
  <div v-for="folder in folders" :key="folder.id" class="details">
    <details v-if="folder.children.length">
      <summary
        @click="handleFolderClick(folder.id)"
        :class="{ selected: chooseFolder === folder.id }"
      >
        {{ folder.name }}
      </summary>
      <FolderTreeComponent
        :folders="folder.children"
        @chooseFolder="handleFolderClick"
      />
    </details>
    <p
      v-else
      @click="handleFolderClick(folder.id)"
      :class="{ selected: chooseFolder === folder.id }"
    >
      {{ folder.name }}
    </p>
  </div>
</template>

<style scoped>
.details,
.details p {
  padding-left: 15px;
}

.details summary,
.details p {
  cursor: pointer;
}

.details summary.selected,
p.selected {
  font-weight: bold;
  color: #007bff;
}
</style>
