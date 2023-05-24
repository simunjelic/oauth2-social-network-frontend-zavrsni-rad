<template>
    <div class="container">
        <InfoMsg v-if="info" :info="info"/>
  <div class="row">
    <div class="col-12">
		<table class="table table-image">
            <thead>
            <tr>
             <th scope="col">Avatar</th>
             <th scope="col">Name</th>
              <th scope="col"></th>
                    
              </tr>
            </thead>
            <tbody>
            <tr v-for="(item) in friends" :key="item.id">
              <td class="w-25" v-if="item.imageUrl">
                  <img v-bind:src="item.imageUrl" class="img-fluid img-thumbnail" alt="Sheep">
             </td>
             <td class="w-25" v-if="item.imageUrl==null">
                  <img src="@/assets/avatar.jpg" class="img-fluid img-thumbnail" alt="Sheep">
             </td>
              <td>{{ item.name }}</td>
              <td><button class="btn btn-primary" @click="unfollow(item.id)">Unfollow</button></td>
              
            </tr>
           
          </tbody>
		</table>   
    </div>

</div>

    </div>    
</template>
<script>
    import axios from 'axios'
    import InfoMsg from '@/components/InfoVue.vue';
    export default {
        name:'FollowingView',
        components: {
          InfoMsg
        },
        created() {
               this.getFriends();
            }
        ,
        data() {
            return {
                friends: '',
                info: ''
            }
        },
        methods: {
           async getFriends() {
               var friends = await axios.get("/friend/search");
                this.friends=friends.data;
                console.log(friends.data);
            },
            async unfollow(id){
                var response = await axios.get("/friend/unfollow/?id="+id);
                this.info=response.data
                
                this.getFriends()
                
            }
        },
        
        

        
        
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