<script setup>
import { ref } from "@vue/reactivity";

defineProps({
  labelName: String,
  type: String,
  name: String,
  placeholder: String,
  value: String,
  isSupriseMe: Boolean,
});


</script>
<template>
  <div>
    <div class="flex items-center gap-2 mb-2">
      <label :for="name" class="block text-sm font-medium text-gray-900">{{
        labelName
      }}</label>
      <div v-if="isSupriseMe">
        <!-- btn that emit clicked on click -->
        <button
          type="button"
          class="font-semibold bg-[#ececf1] text-xs py-1 px-2 rounded-[5px] text-black"
          @click="$emit('handleSupriseMe')"
        >
          Surprise me
        </button>
      </div>
    </div>
    <input
      :type="type"
      :id="name"
      :name="name"
      :placeholder="placeholder"
      :value="value"
      @change="$emit('handleChange')"
      required
      class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-[#6469ff] focus:border-[#6469ff] outline-none block w-full p-3"
    />
  </div>
</template>

<style></style>
