<template>
<main class="form-signin w-100 m-auto container">
    <div class="container">
  <form @submit.prevent="submitLogin">
    <h1 class="h3 mb-3 fw-normal">Please sign in</h1>

    <div class="form-floating">
      <input type="email" class="form-control" v-model="email" id="floatingInput" placeholder="name@example.com">
      <label for="floatingInput">Email address</label>
    </div>
    <div class="form-floating">
      <input type="password" class="form-control" v-model="password" id="floatingPassword" placeholder="Password">
      <label for="floatingPassword">Password</label>
    </div>

    <div class="checkbox mb-3">
      <label>
        <input type="checkbox" value="remember-me"> Remember me
      </label>
    </div>
    <button class="w-100 btn btn-lg btn-primary" type="submit">Sign in</button>
    <p class="mt-5 mb-3 text-muted">&copy; 2017–2022</p>
  </form>
  </div>
</main>
    
</template>

<script>
import axios from 'axios'
    export default {
      
        name: "LoginVue",
        data() {
          return {
            email: '',
            password: ''
          }
        },
        methods: {
         async submitLogin() {
            const response = await axios.post('/auth/login', {
              email: this.email,
              password: this.password
            });
            localStorage.setItem('token', response.data.accessToken);
            
            this.$store.dispatch('user',response.data.user);
            
            
            this.$router.push('/');
                
              
            

             }

        }
    }
</script>

<style scope>
     .form-signin {
  max-width: 330px;
  padding: 15px;
}

.form-signin .form-floating:focus-within {
  z-index: 2;
}

.form-signin input[type="email"] {
  margin-bottom: -1px;
  border-bottom-right-radius: 0;
  border-bottom-left-radius: 0;
}

.form-signin input[type="password"] {
  margin-bottom: 10px;
  border-top-left-radius: 0;
  border-top-right-radius: 0;
}
    </style>