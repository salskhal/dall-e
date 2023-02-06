<script setup>
import { FormFields, Loader } from "@/components";
import { ref } from "@vue/reactivity";
import { useRouter } from "vue-router";
import { preview } from "../assets";

import { getRandomPrompt } from "../utils";

const router = useRouter();

const generatingImg = ref(false);
const loading = ref(false);
const form = ref({
  name: "",
  prompt: "",
  photo: "",
});

const handleSubmit = async (e) => {
  e.preventDefault();

  if (form.value.prompt && form.value.photo) {
    loading.value = true;
    try {
      const response = await fetch("https://dall-e-9xsh.onrender.com/api/v1/post", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify({ ...form.value }),
      });

      await response.json();
      // alert("Success");
      router.push("/");
    } catch (err) {
      alert(err);
    } finally {
      loading.value = false;
    }
  } else {
    alert("Please generate an image with proper details");
  }
};

const handleSupriseMe = () => {
  form.value = { ...form.value, prompt: getRandomPrompt() };
};

const generateImage = async () => {
  if (form.value.prompt) {
    try {
      generatingImg.value = true;
      const response = await fetch("https://dall-e-9xsh.onrender.com/api/v1/dalle", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify({ prompt: form.value.prompt }),
      });
      const data = await response.json();
      form.value = {
        ...form.value,
        photo: `data:image/jpeg;base64,${data.photo}`,
      };
      // form.value = { ...form.value, photo: data.photo };
    } catch (err) {
      console.log(err);
    } finally {
      generatingImg.value = false;
    }
  } else {
    alert("Please enter a prompt");
  }
};
</script>
<template>
  <section class="max-w-7xl mx-auto relative  ">
 
    <div>
      <h1 class="font-extrabold text-[#222328] text-[32px]">Create</h1>
      <p class="mt-2 text-[#666e75] text-[14px] max-w-[500px]">
        Generate an imaginative image through DALL-E AI and share it with the
        community
      </p>
    </div>
    <form class="mt-16 max-w-3xl" @submit="handleSubmit">
      <div class="flex flex-col gap-5">
        <div class="">
          <label for="name" class="block text-sm font-medium text-gray-900">
            Your name
          </label>
          <input
            type="text"
            name="name"
            placeholder="Ex., Khalid Salman"
            class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-[#6469ff] focus:border-[#6469ff] outline-none block w-full p-3"
            v-model="form.name"
            required
          />
        </div>
        <div>
          <div class="flex items-center gap-2 mb-2">
            <label for="prompt" class="block text-sm font-medium text-gray-900">
              Prompt
            </label>
            <button
              class="font-semibold bg-[#ececf1] text-xs py-1 px-2 rounded-[5px] text-black"
              type="button"
              @click="handleSupriseMe"
            >
              Suprise me
            </button>
          </div>
          <input
            type="text"
            name="prompt"
            placeholder="A man wanders through the rainy streets of Lagos, with bright neon signs, 50mm"
            class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-[#6469ff] focus:border-[#6469ff] outline-none block w-full p-3"
            v-model="form.prompt"
            required
          />
        </div>
        <div
          class="relative bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 w-64 p-3 h-64 flex justify-center items-center"
        >
          <img
            v-if="form.photo"
            :src="form.photo"
            :alt="form.prompt"
            class="w-full h-full object-contain"
          />
          <img
            v-else
            :src="preview"
            alt="preview"
            class="w-full h-full object-cover opacity-40"
          />

          <div
            v-if="generatingImg"
            class="absolute inset-0 z-0 flex justify-center items-center bg-[rgba(0,0,0,0.5)] rounded-lg"
          >
            <Loader />
          </div>
        </div>
      </div>
      <div>
        <button
          type="button"
          class="mt-5 bg-[#222328] text-white text-sm font-medium rounded-md w-full sm:w-auto px-5 py-2.5 text-center"
          @click="generateImage"
        >
          {{ generatingImg ? "Generating....." : "Generate Image" }}
        </button>
      </div>
      <div className="mt-10">
        <p className="mt-2 text-[#666e75] text-[14px] ">
          ** Once you have created the image you want, you can share it with
          others in the community **
        </p>
        <button
          type="submit"
          class="mt-3 text-white bg-[#6469ff] font-medium rounded-md text-sm w-full sm:w-auto px-5 py-2.5 text-center"
        >
          {{ loading ? "Sharing..." : "Share with the Community" }}
        </button>
      </div>
    </form>
  </section>
</template>

<style></style>
