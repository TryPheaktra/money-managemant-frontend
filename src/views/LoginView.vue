<!-- src/views/Login.vue -->
<template>
  <div class="min-h-screen flex items-center justify-center bg-gray-100">
    <div class="bg-white p-8 rounded-xl shadow-md w-full max-w-md">
      <h2 class="text-2xl font-bold mb-6 text-center">Login</h2>

      <form @submit.prevent="handleLogin">
        <div class="mb-4">
          <label>Email</label>
          <input
            v-model="email"
            type="email"
            class="w-full p-2 border rounded"
            required
          />
        </div>

        <div class="mb-4">
          <label>Password</label>
          <input
            v-model="password"
            type="password"
            class="w-full p-2 border rounded"
            required
          />
        </div>

        <button
          class="w-full bg-blue-500 text-white p-2 rounded hover:bg-blue-600"
        >
          Login
        </button>
      </form>

      <p class="mt-4 text-center">
        Don't have an account?
        <router-link to="/register" class="text-blue-500">
          Register
        </router-link>
      </p>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import axios from 'axios'
import { useRouter } from 'vue-router'

const email = ref('')
const password = ref('')
const router = useRouter()

const handleLogin = async () => {
  try {
    const res = await axios.post('http://localhost:8787/auth/login', {
      email: email.value,
      password: password.value
    })

    localStorage.setItem('token', res.data.token)

    router.push('/')
  } catch (err: any) {
    alert(err.response?.data?.error || 'Login failed')
  }
}
</script>