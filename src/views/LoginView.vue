<template>
<main class="form-signin w-100 m-auto container">
    <div class="container">
  <form @submit.prevent="submitLogin">
    <ErrorMsg v-if="error" :error="error"/>
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
    
  </form>
   <div class="mt-5">
    <h4>Or sign in with </h4>
    <a class=" w-100 btn btn-danger" href="http://localhost:8080/oauth2/authorize/google?redirect_uri=http://localhost:3000/oauth2/redirect">Google</a>
    <a class="my-1 w-100 btn btn-primary" href="http://localhost:8080/oauth2/authorize/facebook?redirect_uri=http://localhost:3000/oauth2/redirect">Facebook</a>
    <a class="w-100 btn btn-dark" href="http://localhost:8080/oauth2/authorize/github?redirect_uri=http://localhost:3000/oauth2/redirect">GitHub</a>
    
    </div>
  </div>
</main>
    
</template>

<script>
import axios from 'axios'
import ErrorMsg from '@/components/ErrorVue.vue';
    export default {
      
        name: "LoginVue",
        components: {
          ErrorMsg
        },
        data() {
          return {
            email: '',
            password: '',
            error: ''
          }
        },
        methods: {
         async submitLogin() {
          try{
            const response = await axios.post('/auth/login', {
              email: this.email,
              password: this.password
            })
            localStorage.setItem('token', response.data.accessToken);
            
            this.$store.dispatch('user',response.data.user);
            
        
            
            window.location.href = "/"
                
              
            
            }catch(e){
                this.error="Invalid username or password";
            }
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