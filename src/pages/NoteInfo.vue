<template>
  <q-page padding>
    <MainContainer>
        <div v-if="editing">
          <form @submit="editing = false">
            <q-input class="q-mt-sm" filled label="Title" v-model="note.title"/>
            <q-input
              class="q-mt-sm"
              filled
              label="Description"
              v-model="note.description"
              dense
            />

            <q-card flat bordered class="q-mt-sm">
              <q-editor v-model="note.content" min-height="5rem" />
            </q-card>

            <div class="q-mt-md row justify-end">
              <q-btn class="q-ml-sm" type="submit" color="positive" unelevated>Done</q-btn>
            </div>
          </form>
        </div>
        <div v-else>
            <div class="row items-center justify-between">
                <h5>{{ note.title }}</h5>
                <div>
                  <q-btn
                    round
                    color="secondary"
                    icon="edit"
                    @click="editing = true"
                  />
                  <q-btn
                    class="q-ml-sm"
                    round
                    color="red"
                    icon="delete"
                    @click="remove"
                  />
                </div>
            </div>
            <div>{{ note.description }}</div>
            <div class="q-mt-md" v-html="note.content"></div>
        </div>
    </MainContainer>
  </q-page>
</template>

<script setup>
import MainContainer from 'src/components/MainContainer.vue'
import { computed, ref } from 'vue'
import { useLocalNotes } from 'src/helper'
import { useRouter, useRoute } from 'vue-router'

const notes = useLocalNotes()
const route = useRoute()
const noteId = computed(() => parseInt(route.params.id))
const note = computed(() => notes.value[noteId.value])

const router = useRouter()
const remove = () => {
  notes.value.splice(noteId.value, 1)
  router.push('/')
}
const editing = ref(false)

</script>
