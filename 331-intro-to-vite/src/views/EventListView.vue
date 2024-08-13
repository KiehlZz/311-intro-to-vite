<script setup lang="ts">
import EventCard from '@/components/EventCard.vue'
import { type Event } from '@/types'
import { ref, onMounted, computed, watchEffect } from 'vue'
import { useRoute } from 'vue-router'
import EventService from '@/services/EventService'

const route = useRoute()

const events = ref<Event[] | null>(null)
const totalEvents = ref(0)
const perPage = computed(() => parseInt(route.query.perPage as string) || 2)
const page = computed(() => parseInt(route.query.page as string) || 1)
const hasNextPage = computed(() => {
  const totalPages = Math.ceil(totalEvents.value / 3)
  return page.value < totalPages
})

onMounted ( () => {
  watchEffect(() => {
    EventService.getEvents(3, page.value)
      .then((response) => {
        events.value = response.data
        totalEvents.value = parseInt(response.headers['x-total-count'])
      })
      .catch((error) => {
        console.error('There was an error!', error)
      })
  })
})
</script>

<template>
  <h1 class="text-4xl mb-8">Events For Good</h1>
  <div class="flex flex-col items-center">
    <EventCard v-for="event in events" :key="event.id" :event="event"/>
    <div class="flex w-72">
      <RouterLink
        id="page-prev"
        class="flex-1 text-left text-gray-700 font-bold no-underline"
        :to="{ name: 'event-list-view', query: { page: page - 1, perPage: perPage }}"
        rel="prev"
        v-if="page != 1"
        >&#60; Prev Page</RouterLink
      >

      <RouterLink 
        id="page-next"
        class="flex-1 text-left text-gray-700 font-bold no-underline"
        :to="{ name: 'event-list-view', query: { page: page + 1, perPage: perPage }}"
        rel="next"
        v-if="hasNextPage"
        >Next Page &#62;</RouterLink
      >
    </div>
  </div>
</template>
