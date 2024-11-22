<template>
  <header class="bg-white border border-gray-200">
    <div class="max-w-5xl px-6 py-4 mx-auto text-gray-600">
      <div class="sm:flex sm:items-center sm:justify-between">
        <div class="flex items-center gap-4 mb-4 sm:mb-0">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            viewBox="0 0 24 24"
            stroke-width="1.5"
            stroke="currentColor"
            class="size-6 stroke-blue-700"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              d="M2.25 6.75c0 8.284 6.716 15 15 15h2.25a2.25 2.25 0 0 0 2.25-2.25v-1.372c0-.516-.351-.966-.852-1.091l-4.423-1.106c-.44-.11-.902.055-1.173.417l-.97 1.293c-.282.376-.769.542-1.21.38a12.035 12.035 0 0 1-7.143-7.143c-.162-.441.004-.928.38-1.21l1.293-.97c.363-.271.527-.734.417-1.173L6.963 3.102a1.125 1.125 0 0 0-1.091-.852H4.5A2.25 2.25 0 0 0 2.25 4.5v2.25Z"
            />
          </svg>
          <div class="text-lg font-semibold text-gray-600">Contact Management</div>
        </div>
        <div class="relative">
          <input
            v-model="searchTerm"
            @input="handleSearch"
            type="text"
            class="w-full px-4 py-2 text-sm border border-gray-300 rounded-md min-w-64 focus:outline-none"
            placeholder="Search contacts"
          />
          <svg
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            viewBox="0 0 24 24"
            stroke-width="1.5"
            stroke="currentColor"
            class="absolute transform -translate-y-1/2 size-6 top-1/2 right-4"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              d="m21 21-5.197-5.197m0 0A7.5 7.5 0 1 0 5.196 5.196a7.5 7.5 0 0 0 10.607 10.607Z"
            />
          </svg>
        </div>
      </div>
    </div>
  </header>
</template>

<script setup>
import { ref } from "vue";

const emit = defineEmits(["search"]);

const searchTerm = ref("");

const handleSearch = () => {
  emit("search", searchTerm.value);
};
</script>

<style lang="scss" scoped></style>
