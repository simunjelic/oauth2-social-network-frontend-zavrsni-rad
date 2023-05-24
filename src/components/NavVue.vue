<template>
  <nav class="navbar navbar-expand-md navbar-dark bg-dark mb-4">
  <div class="container-fluid">
    <a class="navbar-brand" href="#">ProgresSUM</a>
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarCollapse" aria-controls="navbarCollapse" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarCollapse">
      <ul class="navbar-nav me-auto mb-2 mb-md-0">
        <li class="nav-item">
          <router-link class="nav-link " to="/">Home</router-link>
        </li>
        <li class="nav-item" v-if="user">
          <router-link class="nav-link "  to="/following">Following</router-link>
        </li>
        <li class="nav-item" v-if="user">
          <router-link class="nav-link "  to="/followers">Followers</router-link>
        </li>
        
        <li class="nav-item" v-if="user">
          <router-link class="nav-link "  to="/search">Search</router-link>
        </li>
        
      </ul>
      <!--<form class="d-flex" @submit.prevent="submitSerach" role="search">
        <input class="form-control me-2" v-model="email" type="search" placeholder="Search" aria-label="Search">
        <button class="btn btn-outline-success" type="submit">Search</button>
      </form>-->
      <ul class="navbar-nav mb-2 mb-md-0">
        <li class="nav-item " v-if="!user">
          <router-link class="nav-link " to="/login">Login</router-link>
        </li>
        <li class="nav-item" v-if="!user">
          <router-link class="nav-link "  to="/register">Sign Up</router-link>
        </li>
        <li class="nav-item dropdown" v-if="user">
        <a class="nav-link dropdown-toggle" href="#" id="navbarDropdown" role="button" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
          {{ user.name }}
        </a>
        <div class="dropdown-menu" aria-labelledby="navbarDropdown">
          <a class="dropdown-item" href="#">Action</a>
          <a class="dropdown-item" href="#">Another</a>
          <div class="dropdown-divider"></div>
          <a class="dropdown-item"  href="javascript:void(0)"  @click="handleClick">Logout</a>
        </div>
      </li>
        </ul>
      
    </div>
  </div>
</nav>
</template>

<script>
  import { mapGetters } from 'vuex';
    export default {
        name: 'NavBar',
        data() {
          return {
            name: ''
          }
        },
        methods: {
          handleClick() {
            localStorage.removeItem('token');
            
            this.$store.dispatch('user',null)

            this.$router.push("/login")
          },
          
        },
        computed: {
          ...mapGetters(['user'])
        }
    }
</script>


<style>
 .bd-placeholder-img {
        font-size: 1.125rem;
        text-anchor: middle;
        -webkit-user-select: none;
        -moz-user-select: none;
        user-select: none;
      }

      @media (min-width: 768px) {
        .bd-placeholder-img-lg {
          font-size: 3.5rem;
        }
      }

      .b-example-divider {
        height: 3rem;
        background-color: rgba(0, 0, 0, .1);
        border: solid rgba(0, 0, 0, .15);
        border-width: 1px 0;
        box-shadow: inset 0 .5em 1.5em rgba(0, 0, 0, .1), inset 0 .125em .5em rgba(0, 0, 0, .15);
      }

      .b-example-vr {
        flex-shrink: 0;
        width: 1.5rem;
        height: 100vh;
      }

      .bi {
        vertical-align: -.125em;
        fill: currentColor;
      }

      .nav-scroller {
        position: relative;
        z-index: 2;
        height: 2.75rem;
        overflow-y: hidden;
      }

      .nav-scroller .nav {
        display: flex;
        flex-wrap: nowrap;
        padding-bottom: 1rem;
        margin-top: -1px;
        overflow-x: auto;
        text-align: center;
        white-space: nowrap;
        -webkit-overflow-scrolling: touch;
      }

</style>