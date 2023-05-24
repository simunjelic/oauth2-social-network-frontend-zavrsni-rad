<script>
    export default {
        mounted(){
     var token=this.url_data=this.$route.query.token;
      var error=this.url_data=this.$route.query.error;
     if(token){
       localStorage.setItem('token',token);
        this.$store.dispatch('user',this.$route.query.user);
        window.location.href = "/"
        
     }
     if(error){
        this.$router.push({name: '/login', params: { error: this.error }})
     }
    }

    }
</script>