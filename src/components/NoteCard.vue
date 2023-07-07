<template>
  <q-card flat bordered class="q-mb-sm cursor-pointer" @click="$emit('click', $event)">
    <q-card-section class="q-pt-xs">
      <div class="text-h5 q-mt-sm q-mb-xs">{{ props.title }}</div>
      <div class="text-caption text-grey">{{ props.description }}</div>
    </q-card-section>
  </q-card>
</template>

<script setup>
import { defineProps } from 'vue'
const props = defineProps({
  title: String,
  description: String
})

</script>
