<script setup lang="ts">

import {onMounted, ref} from "vue";

interface ModalProps {
  show: Boolean,
  onShow: () => void
  addDevelopers: () => void
}

const props = defineProps<ModalProps>()

const name = ref('')
const username = ref('')
const email = ref('')
const street = ref('')

const push = () => {
  if (name.value && username.value && email.value && street.value != '') {
    props.onShow()
    const newObj = {name: name.value, username: username.value, email: email.value, address: {street: street.value}}
    props.addDevelopers(newObj)
    name.value = ''
    username.value = ''
    email.value = ''
    street.value = ''
  } else {
    alert('Поля пустые!')
  }
}

</script>

<template>
  <div @click.self="props.onShow(false)"
      class="modal"
      tabindex="-1"
      :style="{
    display: show ? 'block' : 'none'
  }">
    <div class="modal-dialog" @click="closeClick">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title">Modal title</h5>
          <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close" @click="onShow(false)"></button>
        </div>
        <div class="modal-body">
          <div class="form-floating mb-3">
            <input type="text" v-model="name" class="form-control" id="floatingInput" placeholder="Name">
            <label for="floatingInput">Name</label>
          </div>
          <div class="form-floating mb-3">
            <input type="text" v-model="username" class="form-control" id="floatingPassword" placeholder="Username">
            <label for="floatingPassword">Username</label>
          </div>
          <div class="form-floating mb-3">
            <input type="Email" v-model="email" class="form-control" id="floatingPassword" placeholder="Email">
            <label for="floatingPassword">Email</label>
          </div>
          <div class="form-floating mb-3">
            <input type="text" v-model="street" class="form-control" id="floatingPassword" placeholder="Street">
            <label for="floatingPassword">Street</label>
          </div>
        </div>
        <div class="modal-footer">
          <button type="button" class="btn btn-secondary" data-bs-dismiss="modal" @click="onShow(false)">Close</button>
          <button type="button" class="btn btn-primary" @click="push">Save changes</button>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>

</style>