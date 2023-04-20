<script setup>
import { signOut } from '@firebase/auth'
import BaseButton from './base/BaseButton.vue'
import { useCurrentUser, useFirebaseAuth } from 'vuefire'

const user = useCurrentUser()
const auth = useFirebaseAuth()

async function signOutOfFirebase() {
  signOut(auth)
    .then(() => {
      console.log('Logged out!')
    })
    .catch((error) => {
      console.log(error)
    })
}
</script>

<template>
  <v-app-bar color="teal">
    <v-app-bar-title>Vue Eats</v-app-bar-title>
    <v-spacer></v-spacer>
    <nav class="pr-4">
      <BaseButton to="/">Home</BaseButton>
      <BaseButton to="/new">New</BaseButton>
      <BaseButton v-if="user?.email" @click="signOutOfFirebase"
        >Sign-Out</BaseButton
      >
      <BaseButton v-else to="/sign-in">Sign-In</BaseButton>
    </nav>
  </v-app-bar>
</template>

<style></style>
