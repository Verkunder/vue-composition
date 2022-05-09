<script setup lang="ts">
import {onBeforeMount, ref} from "vue";
import axios from "axios"
import TheDevelopersTable from "@/components/TheDevelopersTable.vue";
import AppModal from "@/components/AppModal.vue";

const developers = ref([])

onBeforeMount(  async () => {
  await axios
      .get('https://jsonplaceholder.typicode.com/users')
      .then(response => (developers.value = response.data));
})
</script>

<template>
  <TheDevelopersTable v-if="developers.length" :developers="developers" />
</template>

<style scoped>

</style>
