<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
import { useMessageStore } from './stores/message';
import { storeToRefs } from 'pinia';
import { SpeedInsights } from '@vercel/speed-insights/next';

const store = useMessageStore()
const { message } = storeToRefs(store)
</script>

<template>
  <SpeedInsights />
  <div class="text-center font-sans texe-gray-700 antialiased">
    <header>
      <div id="flashMessage" class="animate-fade" v-if="message">
        <h4>{{ message }}</h4>
      </div>
      <h1>Deploy with Vercel</h1>
      <div class="wrapper">
        <nav class="py-6">
          <RouterLink class="font-bold text-gray-700" exact-active-class="text-green-500" :to="{ name: 'event-list-view', query: { perPage: 2, page: 1 } }">Event</RouterLink> |
          <RouterLink class="font-bold text-gray-700" exact-active-class="text-green-500" :to="{ name: 'about'}">About</RouterLink>
        </nav>
      </div>
    </header>

    <RouterView />
  </div>
</template>
