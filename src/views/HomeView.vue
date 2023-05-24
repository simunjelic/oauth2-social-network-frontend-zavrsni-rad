<template>
  <div class="home">
    <h3 v-if="!user">You are not logged in</h3>


    <div class="container">
        <!-- Edit modal -->
            
            <div class="modal fade" id="exampleModal" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
  <div class="modal-dialog" role="document">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title" id="exampleModalLabel">Edit post</h5>
        <button type="button" class="close" data-dismiss="modal" aria-label="Close">
          <span aria-hidden="true">&times;</span>
        </button>
      </div>
      <div class="modal-body">
        <form @submit.prevent="submitUpdate">
          <div class="form-group">
            <textarea class="form-control" id="message-text" v-model="editText"></textarea>
          </div>
          <div class="modal-footer">
        <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
        <button type="submit" class="btn btn-primary" >Edit post</button>
      </div>
        </form>
      </div>
      
    </div>
  </div>
</div>


          <div v-if="user" class="row justify-content-start mb-5">
             <div class="col-3" v-if="user.imageUrl!=null">
                <img  :src="user.imageUrl" alt="" class="loginAvatar rounded-circle">   <span class="ime">{{ user.name }}</span>
             </div>
              <div class="col-3" v-if="user.imageUrl==null">
                <img  src="@/assets/avatar.jpg" alt="" class="loginAvatar rounded-circle">   <span class="ime">{{ user.name }}</span>
              </div>
              <div class="col-6">
                <form  @submit.prevent="addPost">
                  <input type="text" class="form-control" v-model="message" placeholder="What's on your mind?"/>
                </form>
                
                </div>
          </div>
        

        
            <div class="row main-row well bg-white rounded my-3 shadow" 
            v-for="(item) in data" :key="item.id">
              <div class="dropdown menu d-flex flex-row-reverse">
                        <button class="btn btn-white dropdown-toggle" type="button" id="dropdownMenuButton" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
   
                                </button>
                                <div class="dropdown-menu" aria-labelledby="dropdownMenuButton">
                                  <a class="dropdown-item" v-if="user.id==item.user.id" @click="updatePost(item.id,item.content)"
                                  data-toggle="modal" data-target="#exampleModal"  href="#">Edit</a>
                                  <a class="dropdown-item" href="#">Report</a>
                                  <a class="dropdown-item" v-if="user.id==item.user.id" @click="deletePost(item.id)" href="#">Delete</a>
                                  
                                  
                                  
                                  
                                </div>
                              </div>
                <div class="col-lg-12 col-md-12 col-sm-12 col-3">
                    <div class="col-3" v-if="item.user.imageUrl!=null">
                <img  :src="item.user.imageUrl" alt="" class="loginAvatar rounded-circle mx-3">   <span class="ime">{{ item.user.name }}</span>
             </div>
              <div class="col-lg-12 col-md-12 col-sm-12 col-3" v-if="item.user.imageUrl==null">
                <img  src="@/assets/avatar.jpg" alt="" class="loginAvatar rounded-circle">   <span class="ime">{{ item.user.name }}</span>
              </div>    
                </div>
                <div class="col-lg-9 col-md-12 col-sm-12 py-1">
                    <div class="blog-title">
                        <h3 class=" fw-bold"><a href="#" class="text-decoration-none text-dark">{{ item.name }}</a></h3>
                        
                    </div>
                    
                
                    <div class="pb-2  w-100">
                        <div class="tt"> {{ item.content }}</div>
                    </div>
                    
                    
                </div>

            

              </div>          
          
                

    </div>

    
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
import axios from 'axios'
export default {
  name: 'HomeView',
  data() {
    return {
      message: '',
      data: '',
      editText: '',
      editId: '',
    }
  },
  created(){
    this.getPosts()
    
  },

  computed: {
          ...mapGetters(['user'])
        },
  methods: {
      async addPost(){
        if(this.message!=null){
        await axios.post('/addPost',{
            content: this.message,
            })
            this.message=""
            this.getPosts()
          }
      },
      async getPosts(){
        const response = await axios.get('/getPosts')
        this.data=response.data
        console.log(response.data)
      },
      async deletePost(id){
          var response = await axios.get("/delete/post/?id="+id);
                console.log(response.data)

          this.getPosts()
                     
      },
      updatePost(id,content){
        this.editText=content
        this.editId=id
      },
      async submitUpdate(){
        
        const response = await axios.post('/edit/post', {
              id: this.editId,
              content: this.editText
            })
          console.log(response.data)
          this.editId='';
          this.editText='';
          this.$router.go()
      },
    
     
       
       }
       
      

  }
 
  
  

</script>


<style scoped>
.ime {
  font-size: 20px;
}
.loginAvatar {
 height: 50px;
 widows: 50px;
}
input {
  background-color: white;
  background-position: 10px 10px;
  background-repeat: no-repeat;
  padding-left: 40px;
  height: 60px;
  width:100%;
}
.tt {
  margin-left: 15%;
}

</style>
