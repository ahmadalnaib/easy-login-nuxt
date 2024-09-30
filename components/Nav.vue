<template>
  <div>

  <nav>
    <ul>
      <li>
        <nuxt-link to="/login">Login</nuxt-link>
      </li>
      <li>
        <nuxt-link to="/register">Register</nuxt-link>
      </li>

      <li>
        <nuxt-link to="/login" @click="logout">Logout</nuxt-link>
      </li>
      <li>
       <a href="">     {{ name }}</a>
      </li>
    </ul>
  </nav>

</div>
</template>

<script setup lang="ts">
import axios from 'axios';

const name=ref('')


onMounted(async() => {
  const { data }=await axios.get('http://localhost:8001/api/user', { withCredentials: true });

  name.value=data.first_name;

});

const logout = async () => {
  try {
    await axios.post('http://localhost:8001/api/logout', {}, { withCredentials: true });
   
  } catch (error) {
    console.error(error);
  }
};

</script>