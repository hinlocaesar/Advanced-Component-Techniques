<script setup>
/*
1) Done-Parent Component pass data to child when button is pressed
2) Child does not change state of parent
    -create local copy to copy state from parent to child
    -link the localstate to inputs
    -on the handleSubmit they you will assign the child to parent value
*/

import {ref,watch} from 'vue'

// 1. Define the models for username and password
const username = defineModel('username')
const password = defineModel('password')

const localUsername = ref(username.value)
const localUserpass = ref(password.value)


watch(username.value, ()=>console.log("HINLO:",localusername))

watch(username, (newValue) => {
  localUsername.value = newValue
})

watch(password, (newValue) => {
  localUserpass.value = newValue
})


const handleSubmit = () => {

  console.log("Hinlo handleSubmit is called")
  username.value  =   localUsername.value
  password.value = localUserpass.value
}


</script>

<template>
  <form @submit.prevent="handleSubmit" class="form"> 
    <h1>Login</h1>

    <label>
      <span>Username</span>
      <input type="text" v-model="localUsername" />
    </label>

    <label>
      <span>Password</span>
      <input type="password" v-model="localUserpass" />
    </label>

    <button type="submit">Login</button>
  </form>
</template>

<style scoped>
.form {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}
label {
  display: flex;
  flex-direction: column;
  font-size: 0.9rem;
}
input {
  padding: 0.4rem;
  border-radius: 4px;
  border: 1px solid #ccc;
}
button {
  margin-top: 0.5rem;
  padding: 0.5rem 1rem;
  border: none;
  background-color: #42b983;
  color: white;
  border-radius: 6px;
  cursor: pointer;
}
button:hover {
  background-color: #36986b;
}
</style>