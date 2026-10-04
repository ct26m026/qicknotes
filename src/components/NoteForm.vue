<script setup>
import { ref } from 'vue'

const emit = defineEmits(['add-note'])

const title = ref('')
const content = ref('')
const tags = ref('')

function submitForm() {
  if (!title.value.trim() || !content.value.trim()) {
    return
  }

  const newNote = {
    title: title.value.trim(),
    content: content.value.trim(),
    tags: tags.value
      .split(',')
      .map(tag => tag.trim())
      .filter(tag => tag.length > 0)
  }

  emit('add-note', newNote)

  title.value = ''
  content.value = ''
  tags.value = ''
}
</script>

<template>
  <form @submit.prevent="submitForm">
    <input
      v-model="title"
      type="text"
      placeholder="Titel"
    >

    <textarea
      v-model="content"
      placeholder="Text"
      rows="5"
    ></textarea>

    <input
      v-model="tags"
      type="text"
      placeholder="Tags, durch Komma getrennt"
    >

    <button type="submit">
      Notiz hinzufügen
    </button>
  </form>
</template>

<style scoped>
form {
  display: flex;
  flex-direction: column;
  gap: 10px;
  margin-bottom: 30px;
}

input,
textarea {
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 6px;
  font-family: inherit;
}

button {
  align-self: flex-start;
  padding: 10px 16px;
  cursor: pointer;
}
</style>