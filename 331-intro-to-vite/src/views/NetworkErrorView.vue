<template>
    <div class="text-center py-20">
      <h1 class="text-4xl font-bold mb-4">Uh-Oh!</h1>
      <h3 class="text-lg">
        It looks like you're experiencing some network issues, please take a breath and
        <a href="#" class="text-blue-500 underline" @click="$router.go(-1)">click here</a> to try again.
      </h3>
    </div>
  </template>