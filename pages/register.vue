<template>
  <div>
    <h1>Register</h1>
    <form @submit.prevent="register">
      <input type="text" v-model="first_name" placeholder="First_name" />
      <input type="text" v-model="last_name" placeholder="Last_name" />
      <input type="text" v-model="email" placeholder="Email" />

      <input type="password" v-model="password" placeholder="Password" />
      <input type="password" v-model="confirm_password" placeholder="Confirm Password" />
      <button type="submit">Register</button>
    </form>
  </div>
</template>
<script lang="ts" setup>

import axios from 'axios';

const first_name = ref('');
const last_name = ref('');
const email = ref('');
const password = ref('');
const confirm_password = ref('');
const router = useRouter();

const register = async () => {
  try {
    await axios.post('http://localhost:8001/api/register', {
      first_name: first_name.value,
      last_name: last_name.value,
      email: email.value,
      password: password.value,
      confirm_password: confirm_password.value
    });
    await router.push('/login');
  } catch (error) {
    if (axios.isAxiosError(error)) {
      console.error('Registration failed:', error.response?.data || error.message);
    } else {
      console.error('An unexpected error occurred:', error);
    }
  }
};
</script>