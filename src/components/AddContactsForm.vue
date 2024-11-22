<template>
  <div class="max-w-5xl px-6 py-4 mx-auto">
    <div class="flex items-center justify-end">
      <button
        @click="showModal = true"
        class="flex items-center justify-end gap-1 px-4 py-2 text-white transition-colors duration-200 bg-blue-600 border border-transparent rounded-md focus:bg-blue-700 hover:bg-blue-700 focus:ring focus:ring-blue-700 focus:ring-offset-1"
      >
        <svg
          xmlns="http://www.w3.org/2000/svg"
          fill="none"
          viewBox="0 0 24 24"
          stroke-width="1.5"
          stroke="currentColor"
          class="size-4"
        >
          <path stroke-linecap="round" stroke-linejoin="round" d="M12 4.5v15m7.5-7.5h-15" />
        </svg>

        Add new contact
      </button>
    </div>
    <teleport to="body">
      <div v-if="showModal" class="absolute top-0 left-0 flex items-center justify-center w-full h-full bg-gray-800/60">
        <div class="p-6 text-gray-600 bg-gray-100 rounded-md">
          <div class="flex items-center justify-between mb-6">
            <h1 class="text-xl font-semibold">New contact details</h1>
            <svg
              @click="showModal = false"
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 24 24"
              stroke-width="1.5"
              stroke="currentColor"
              class="text-gray-500 size-6 hover:text-gray-600"
            >
              <path stroke-linecap="round" stroke-linejoin="round" d="M6 18 18 6M6 6l12 12" />
            </svg>
          </div>

          <form @submit.prevent="submitContact">
            <div class="space-y-4">
              <div>
                <label for="name" class="text-sm font-medium"> Full name </label>
                <div class="mt-1.5">
                  <input
                    v-model="contactData.name"
                    type="text"
                    placeholder="Enter your full name"
                    class="block w-full p-2 transition-all duration-200 border border-gray-200 rounded-md focus:border-blue-600 focus:bg-white"
                  />
                  <span v-if="errors.name" class="text-sm text-red-600">{{ errors.name }}</span>
                </div>
              </div>

              <div>
                <label for="phone" class="text-sm font-medium"> Phone number </label>
                <div class="mt-1.5">
                  <input
                    v-model="contactData.phone"
                    type="text"
                    placeholder="Enter your phone number"
                    class="block w-full p-2 transition-all duration-200 border border-gray-200 rounded-md focus:border-blue-600 focus:bg-white"
                  />
                  <span v-if="errors.phone" class="text-sm text-red-600">{{ errors.phone }}</span>
                </div>
              </div>
            </div>
            <div class="flex justify-end gap-4 mt-10">
              <button
                type="button"
                @click="showModal = false"
                class="px-4 py-2 text-gray-600 transition-colors duration-200 rounded-md hover:bg-gray-100"
              >
                Cancel
              </button>
              <button
                type="submit"
                class="px-4 py-2 font-semibold text-white duration-200 bg-blue-600 border border-transparent rounded-md transition-color hover:bg-blue-700 focus:bg-blue-700"
              >
                Create contact
              </button>
            </div>
          </form>
        </div>
      </div>
    </teleport>
  </div>
</template>

<script setup>
import { reactive, ref, watch } from "vue";
const showModal = ref(false);

const emit = defineEmits(["addContact"]);

const contactData = reactive({ name: "", phone: "" });

const errors = reactive({ name: "", phone: "" });

const validateForm = () => {
  let isValid = true;

  if (!contactData.name.trim()) {
    errors.name = "Full Name is required.";
    isValid = false;
  }
  if (!contactData.phone.trim()) {
    errors.phone = "Phone Number is required.";
    isValid = false;
  }
  return isValid;
};
const submitContact = () => {
  if (validateForm()) {
    const newContact = {
      id: Date.now(),
      ...contactData
    };
    emit("addContact", newContact);

    contactData.name = "";
    contactData.phone = "";
    showModal.value = false;
  }
};
watch(showModal, (newValue) => {
  if (!newValue) {
    errors.name = "";
    errors.phone = "";
  }
});
</script>

<style scoped></style>
