<template>
  <div>
    <h1>Message depuis le backend :</h1>
    <p>{{ message }}</p>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";

const message = ref("Chargement...");

onMounted(async () => {
  try {
    const response = await fetch(`${import.meta.env.VITE_API_URL}`);
    if (response.ok) {
      const data = await response.json();
      message.value = data.message;
    } else {
      message.value = "Erreur lors de l'appel à l'API.";
    }
  } catch (error) {
    message.value = "Erreur de connexion au backend.";
    console.error(error);
  }
});
</script>
