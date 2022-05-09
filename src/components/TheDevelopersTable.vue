<template>
  <div class="container justify-content-center pt-5">
    <div class="row">
      <div class="col">
      </div>
      <div class="col">
        <h1 class="text-center">Таблица с данными</h1>
      </div>
      <div class="col">
        <button type="button" class="btn btn-success" @click="show=true">Success</button>
      </div>
    </div>
    <hr />
    <table class="table" v-if="developers.length">
      <thead>
      <tr>
        <th scope="col">#</th>
        <th scope="col" @click="filtered('name')">Name</th>
        <th scope="col" @click="filtered('username')">Username</th>
        <th scope="col" @click="filtered('email')">Email</th>
        <th scope="col">Street</th>
        <th scope="col"><button v-if="clean" @click="cleanChange" type="button" class="btn btn-danger">Clean</button></th>
      </tr>
      </thead>
      <tbody>
        <TheDeveloperItem v-for="{name, username, email, id, address:{street}} in developers"
                          :name="name"
                          :username="username"
                          :email = 'email'
                          :id="id"
                          :street="street"
                          :remove="remove"
        />
      </tbody>
    </table>
    <h2 v-else class="text-center">Тут ничего нет</h2>
    <AppModal :show="show" :onShow="onShow" :addDevelopers="addDevelopers"/>
  </div>
</template>

<script setup lang="ts">
import TheDeveloperItem from "@/components/TheDeveloperItem.vue";
import AppModal from '@/components/AppModal.vue'
import {onMounted, onUpdated, reactive, ref} from "vue";


interface DevelopersProps {
  developers: [],
}
const props = defineProps<DevelopersProps>()
const developers = ref(props.developers)
const active = ref(false)
const clean = ref(false)
const show = ref(false)

const remove = (idx: number) => {
  const newItem = developers.value.filter(({id}) => {
    return id !== idx
  })
  developers.value = [...newItem]
}

const filtered = (key: keyof DevelopersProps) => {
  developers.value.sort((a, b) => {
    if (active.value) {
      if (a[key] > b[key]) {
        return 1
      }
      if (a[key] < b[key]) {
        return -1
      }
    } else {
      if (a[key] > b[key]) {
        return -1
      }
      if (b[key] > a[key]) {
        return 1
      }
    }
    return 0
  })
  active.value = !active.value
  clean.value = true
}

const cleanChange = () => {
  developers.value.sort((a, b) => {
    if (a.id > b.id) {
      return 1
    } else {
      return -1
    }
    return 0
  })
  clean.value = false
}

const onShow = (value: boolean) => {
  show.value = value
}

const addDevelopers = (item: object) => {
  const idx = developers.value.length + 1
  const add = [...developers.value, {...item, id: idx}]
  developers.value = [...add]
}

</script>

<style scoped>
.custom {
  display: flex;
  justify-content: flex-end;
  align-items: center;
}
</style>