<template>
  <div>
    <div v-if="data.length > 0" class="grid lg:grid-cols-4 sm:grid-cols-3 xs:grid-cols-2 grid-cols-1 gap-3">
      <div
        v-for="post in data"
        :key="post.id"
        class="rounded-xl group relative shadow-card hover:shadow-carhover card"
      >
        <img
          :src="post.photo"
          :alt="post.prompt"
          class="w-full h-auto object-cover rounded-xl"
        />
        <div class="g group-hover:flex flex-col max-h-[94.5%] hidden absolute bottom-0 left-0 right-0 bg-[#10131f] m-2 p-4 rounded-md">
          <p class="text-white text-sm overflow-y-auto">{{ post.prompt }}</p>
          <div class="mt-5 flex justify-between items-center gap-2">
        <div class="flex items-center gap-2">
          <div class="w-7 h-7 rounded-full object-cover bg-green-700 flex justify-center items-center text-white text-xs font-bold">{{post.name[0]}}</div>
          <p class="text-white text-sm">{{post.name}}</p>
        </div>
        <button type="button" @click="downloadFile(post.name, post.photo)"  class="outline-none bg-transparent border-none">
          <img :src=download alt="download" class="w-6 h-6 object-contain invert" />
        </button>
      </div>
        </div>
      </div>
    </div>
    <h2 v-else class="mt-5 font-bold text-[#6469ff] text-xl uppercase">
      {{ title }}
    </h2>
  </div>
</template>

<script setup>
import { ref } from "@vue/reactivity";
import { Cards } from "@/components";
import { download } from "../assets";
import { downloadFile } from "../utils";

defineProps({
  title: String,
  data: Array,
});
</script>

<style></style>
