<template>
  <NavVue />
  <div class="container">
    <router-view />
  </div>
  
</template>

<script>
  import NavVue from './components/NavVue.vue'
  import axios from 'axios'
  
export default {
  
  name: 'App',
  components: {
    NavVue,
  },
  
   async created() {
    const response = await axios.get('user/me');

    this.$store.dispatch('user',response.data);
  }
  
}
</script>
