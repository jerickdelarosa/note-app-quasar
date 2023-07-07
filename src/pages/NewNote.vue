<template>
  <q-page padding>
    <MainContainer>
      <h5>New Note</h5>
      <form @submit="submit">
        <q-input class="q-mt-sm" outlined label="Title" v-model="note.title"/>
        <q-input
          class="q-mt-sm"
          outlined
          label="Description"
          v-model="note.description"
          dense
        />

        <q-card flat bordered class="q-mt-sm">
          <q-editor v-model="note.content" min-height="5rem" />
        </q-card>

        <div class="q-mt-md row justify-end">
          <q-btn to="/" type="reset" flat>Cancel</q-btn>
          <q-btn class="q-ml-sm" type="submit" color="positive" unelevated>Create</q-btn>
        </div>

      </form>
    </MainContainer>
  </q-page>
</template>

<script setup>
import MainContainer from 'src/components/MainContainer.vue'
import { reactive } from 'vue'
import { useLocalNotes } from 'src/helper'
import { useRouter } from 'vue-router'

const notes = useLocalNotes()
const router = useRouter()

const note = reactive({
  title: '',
  description: '',
  content: ''
})

const submit = () => {
  notes.value.unshift({
    ...note,
    createdAt: Date.now(),
    updatedAt: Date.now()
  })

  router.push('/')

  note.title = ''
  note.description = ''
  note.content = ''
}
</script>
