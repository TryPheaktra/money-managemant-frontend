<!-- src/views/Register.vue -->
<template>
  <div class="min-h-screen flex items-center justify-center bg-gray-100">
    <div class="bg-white p-8 rounded-xl shadow-md w-full max-w-md">
      <h2 class="text-2xl font-bold mb-6 text-center">Register</h2>

      <form @submit.prevent="handleRegister">
        <div class="mb-4">
          <label>Name</label>
          <input v-model="name" class="w-full p-2 border rounded" required />
        </div>

        <div class="mb-4">
          <label>Email</label>
          <input v-model="email" type="email" class="w-full p-2 border rounded" required />
        </div>

        <div class="mb-4">
          <label>Password</label>
          <input v-model="password" type="password" class="w-full p-2 border rounded" required />
        </div>

        <button
          class="w-full bg-green-500 text-white p-2 rounded hover:bg-green-600"
        >
          Register
        </button>
      </form>

      <p class="mt-4 text-center">
        Already have an account?
        <router-link to="/" class="text-blue-500">
          Login
        </router-link>
      </p>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import axios from 'axios'
import { useRouter } from 'vue-router'

const name = ref('')
const email = ref('')
const password = ref('')
const router = useRouter()

const handleRegister = async () => {
  try {
    await axios.post('http://localhost:8787/auth/register', {
      name: name.value,
      email: email.value,
      password: password.value
    })

    alert('Register success')
    router.push('/login')
  } catch (err: any) {
    alert(err.response?.data?.error || 'Register failed')
  }
}
</script>