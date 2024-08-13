<script setup lang="ts">
import { defineProps, withDefaults } from 'vue';
const props = withDefaults(
    defineProps<{
        resource: string
    }>(),
    {
        resource: 'page'
    }
)
</script>

<template>
    <div class="text-center py-20">
      <h1 class="text-4xl font-bold mb-4">Oops!</h1>
      <h3 class="text-lg mb-4">The {{ resource }} you're looking for is not here.</h3>
      <router-link :to="{ name: 'event-list-view' }">Back to the home page</router-link>  
    </div>
</template>