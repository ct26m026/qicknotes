<script setup>
import { ref } from 'vue'

import NoteForm from './components/NoteForm.vue'
import NoteCard from './components/NoteCard.vue'
import SearchBar from './components/SearchBar.vue'

import { useNotes } from './composables/useNotes.js'

const searchTerm = ref('')

const {
  addNote,
  deleteNote,
  filteredNotes
} = useNotes()

const visibleNotes = filteredNotes(searchTerm)
</script>

<template>
  <main>
    <h1>QuickNotes</h1>

    <NoteForm @add-note="addNote" />

    <SearchBar v-model="searchTerm" />

    <section>
      <NoteCard
        v-for="note in visibleNotes"
        :key="note.id"
        :note="note"
        @delete="deleteNote"
      />

      <p v-if="visibleNotes.length === 0">
        Keine Notizen gefunden.
      </p>
    </section>
  </main>
</template>

<style>
body {
  margin: 0;
  font-family: Arial, sans-serif;
  background: #f5f5f5;
}

main {
  max-width: 800px;
  margin: 0 auto;
  padding: 30px 20px;
}

h1 {
  margin-bottom: 30px;
}
</style>