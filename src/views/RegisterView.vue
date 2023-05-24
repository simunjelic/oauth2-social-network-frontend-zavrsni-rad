<template>
<main class="form-signin w-100 m-auto container">
    <div class="container">
  <form @submit.prevent="handleSubmit">
  <ErrorMsg v-if="error" :error="error"/>
    <h1 class="h3 mb-3 fw-normal">Please sign up</h1>

    <div class="form-floating">
      <input type="text" class="form-control" v-model="name" id="floatingInput" placeholder="+name">
      <label for="floatingInput">name</label>
    </div>
    <div class="form-floating">
      <input type="email" class="form-control" v-model="email" id="floatingInput" placeholder="name@example.com">
      <label for="floatingInput">Email address</label>
    </div>
    <div class="form-floating">
      <input type="password" class="form-control" v-model="password" id="floatingPassword" placeholder="Password">
      <label for="floatingPassword">Password</label>
    </div>
    <div class="form-floating">
      <input type="password" class="form-control" v-model="confirmPassword" id="checkPassword" placeholder="Password confirm">
      <label for="floatingPassword">Password confim</label>
    </div>

    <div class="checkbox mb-3">
      <label>
        <input type="checkbox" value="remember-me"> Remember me
      </label>
    </div>
    <button class="w-100 btn btn-lg btn-primary" type="submit">Sign up</button>
    <p class="mt-5 mb-3 text-muted">&copy; 2017–2022</p>
  </form>
 
  </div>
</main>
    
</template>

<script>
import axios from 'axios'
import ErrorMsg from '@/components/ErrorVue.vue';
    export default {
        name: "RegisterVue",
        components: {
          ErrorMsg
        },
        data() {
          return {
            name: "",
            email: "",
            password: "",
            confirmPassword: "",
            error: ""
          }
        },
        methods: {
         async handleSubmit(){
            try{
            const response = await axios.post('auth/signup',{
            name: this.name,
            email: this.email,
            password: this.password
            })
              console.log(response)
              this.$router.push('/login')
            }catch(e){
              this.error="Error ocured!"
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