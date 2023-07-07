<template>
  <q-page padding>
      <MainContainer>
          <div class="row items-center justify-between">
            <h5>Your notes</h5>
            <div>
              <q-btn round color="positive" icon="add" to="/new"></q-btn>
            </div>
          </div>

          <NoteCard
            v-for="({ title, description}, idx) in notes"
            :key="idx"
            :title="title"
            :description="description"
            @click="router.push(`/note/${idx}`)"
          />

          <div v-if="notes.length === 0">You have not created any ntoes.</div>
      </MainContainer>
  </q-page>
</template>

<script setup>
import MainContainer from 'src/components/MainContainer.vue'
import NoteCard from 'src/components/NoteCard.vue'
import { useLocalNotes } from 'src/helper'
import { useRouter } from 'vue-router'

const notes = useLocalNotes()
const router = useRouter()

</script>
