<template>
  <tr>
    <th scope="row">{{ id }}</th>
    <td>{{ name }}</td>
    <td>{{username}}</td>
    <td>{{email}}</td>
    <td>{{street}}</td>
    <td><button type="button" class="btn btn-danger" @click="props.remove(id)">Delete</button></td>
  </tr>
</template>

<script setup lang="ts">

interface DeveloperItemProps {
  name: string,
  username: string,
  email: string,
  id: number,
  street: string,
  remove: () => void

}

const props = defineProps<DeveloperItemProps>()

</script>

<style scoped>

</style>