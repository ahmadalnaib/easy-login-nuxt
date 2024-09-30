<template>
  <div>
    <h1>Login</h1>
    <form @submit.prevent="login">
      <input type="text" v-model="form.email" placeholder="Email" />
      <input type="password" v-model="form.password" placeholder="Password" />
      <button type="submit">Login</button>
    </form>
  </div>
</template>

<script lang="ts" setup>
import axios from 'axios';
const router = useRouter();

const form=reactive({
  email:'',
  password:''
})

    const login = async () => {
      try {
        await axios.post('http://localhost:8001/api/login', {
          email: form.email,
          password: form.password
        },{withCredentials:true});
        await router.push('/')
      
      } catch (error) {
        console.error(error)
      }
    }


</script>