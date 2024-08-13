<script setup lang="ts">
import { ref } from 'vue'
import { type Event } from '@/types'
defineProps<{
  event: Event
}>()

</script>

<template>
  <RouterLink class="no-underline text-gray-700" :to="{name: 'event-detail-view', params: {id: event.id} }">
    <div class="cursor-pointer border border-gray-600 p-4 w-64 mb-6 hover:scale-101 hover:shadow-sp">
      <h2 class="text-[20px]">{{ event.title }}</h2>
      <span>@{{ event.time }} on {{ event.date }}</span>
    </div>
  </RouterLink>
</template>
