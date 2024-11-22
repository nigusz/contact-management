<template>
  <div class="min-h-screen bg-gray-100">
    <AppHeader @search="setSearchTerm" />
    <AddContactsForm @addContact="addNewContact" />
    <ContactList :contacts="filteredContacts" />
  </div>
</template>
<script setup>
import { ref, computed, onMounted } from "vue";
import AppHeader from "./components/AppHeader.vue";
import ContactList from "./components/ContactList.vue";
import AddContactsForm from "./components/AddContactsForm.vue";

const contacts = ref([]);
const searchTerm = ref("");

const filteredContacts = computed(() =>
  contacts.value.filter((contact) => contact.name.toLowerCase().includes(searchTerm.value.toLowerCase()))
);

const addNewContact = (contact) => {
  contacts.value.push(contact);
  saveContactsToLocalStorage();
};

const setSearchTerm = (term) => {
  searchTerm.value = term;
};

const saveContactsToLocalStorage = () => {
  localStorage.setItem("contacts", JSON.stringify(contacts.value));
};

const loadContactsFromLocalStorage = () => {
  const savedContacts = JSON.parse(localStorage.getItem("contacts")) || [];
  contacts.value = savedContacts;
};

onMounted(() => {
  loadContactsFromLocalStorage();
});
</script>
<style scoped></style>
