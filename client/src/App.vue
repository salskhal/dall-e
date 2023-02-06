<script setup>
import { RouterLink, RouterView } from "vue-router";
import { logo } from "./assets";
</script>

<template>
  <div>
    <header
      class="w-full flex justify-between items-center bg-white sm:px-8 px-4 py-4 border-b border-b-[#e6ebf4]"
    >
      <router-link to="/">
        <img :src="logo" alt="logo" class="w-28 object-contain" />
      </router-link>

      <router-link
        to="/create-post"
        class="font-inter font-medium bg-[#6469ff] text-white px-4 py-2 rounded-md"
        >Create</router-link
      >
    </header>
    <main class="sm:p-8 px-4 py-8 w-full bg-[#f9fafe] min-h-[calc(100vh-73px)]">
      <RouterView />
    </main>
  </div>
</template>

<style></style>
