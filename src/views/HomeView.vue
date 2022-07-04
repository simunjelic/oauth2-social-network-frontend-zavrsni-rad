<template>
  <div class="home">
    <h3 v-if="user">Hi, {{ user.name }}</h3>
    <h3 v-if="!user">You are not logged in</h3>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
export default {
  name: 'HomeView',
  computed: {
          ...mapGetters(['user'])
        },
  
  
  
}
</script>
