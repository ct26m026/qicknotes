<script setup>
import BaseCard from './BaseCard.vue'

defineProps({
  note: {
    type: Object,
    required: true
  }
})

const emit = defineEmits(['delete'])
</script>

<template>
  <BaseCard>
    <template #header>
      {{ note.title }}
    </template>

    <p>{{ note.content }}</p>

    <div v-if="note.tags.length" class="tags">
      <span
        v-for="tag in note.tags"
        :key="tag"
        class="tag"
      >
        #{{ tag }}
      </span>
    </div>

    <button @click="emit('delete', note.id)">
      Löschen
    </button>
  </BaseCard>
</template>

<style scoped>
.tags {
  display: flex;
  flex-wrap: wrap;
  gap: 6px;
  margin: 12px 0;
}

.tag {
  padding: 4px 8px;
  border-radius: 4px;
  background: #eee;
  font-size: 14px;
}

button {
  cursor: pointer;
}
</style>