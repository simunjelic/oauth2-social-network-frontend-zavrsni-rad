<template>
    <div class="container">
        <h3 class="my-2">Search for friends</h3>
        <form @submit.prevent="getData">
        <input type="search" class="form-control" v-model="search" style="width:30%;display:inline"/>
        <input type="submit" class="btn btn-primary m-2" style="width:10%;display:inline" value="Search">
        </form>
        
<div class="row">
    <div class="col-12">
		<table class="table table-image">
            <thead>
            <tr>
             <th scope="col">Avatar</th>
             <th scope="col">Name</th>
              <th scope="col">.</th>
                    
              </tr>
            </thead>
            <tbody>
              
            <tr  v-for="(item) in data" :key="item.id">
              <td class="w-25" v-if="item.imageUrl">
                  <img v-bind:src="item.imageUrl" class="img-fluid img-thumbnail" alt="Sheep">
             </td>
             <td class="w-25" v-if="item.imageUrl==null">
                  <img src="@/assets/avatar.jpg" class="img-fluid img-thumbnail" alt="Sheep">
             </td>
              <td>{{ item.name }}</td>
              <td><button class="btn btn-primary" @click="follow(item.id)">follow</button></td>
              
            </tr>
           
          </tbody>
		</table> 
    </div>  
    </div>
    </div>

    
</template>

<script>
import axios from 'axios'
import { mapGetters } from 'vuex';
    export default {
        name: 'SearchView',
        data() {
            return {
                search: '',
                data: '',
                friends: ''
            }
        },
        methods: {
            async getData() {
               var response = await axios.get("/user/search/?name="+this.search);
                this.data=response.data
                
            },
            async follow(id) {
               var response = await axios.get("/friend/follow/?id="+id);
                
                console.log(response.data)
                this.$router.push("/");
            }
        },
        computed: {
          ...mapGetters(['user'])
        }
        
        
    }
</script>
<style scoped>
.container {
  padding: 2rem 0rem;
}

h4 {
  margin: 2rem 0rem 1rem;
}
img {
    height: 150px;
    width: 150px;
}


</style>