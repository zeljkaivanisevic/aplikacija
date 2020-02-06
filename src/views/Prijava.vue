<template>
  <div class="pozadina">
    <div class="login">
      <div class="naslov">
        <h1>Prijava</h1>
      </div>
      <form @submit.prevent="login">
        <div class="form-group">
          <input v-model="email" type="email" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp" placeholder="Unesi email">
        </div>
        <div class="form-group">
          <input v-model="password" type="password" class="form-control" id="exampleInputPassword1" placeholder="Unesi lozinku">
        </div>
        <div class="eror" v-if="errorMessage">
            {{ "Lozinka nije ispravna. Pokušajte ponovo." }}
          </div>
        
        <button type="submit" class="btn btn primary"><strong>Prijavi se</strong></button>
      </form>
    </div>
  </div>    
</template>

<script>
export default {
   data (){
    return{
      email:'',
      password:'',
      errorMessage: ""
    }
  },
  methods: {
    login () {
      firebase.auth().signInWithEmailAndPassword(this.email, this.password).then(function() {   
        }).catch(error => {
          this.errorMessage = error.message;
          
        });
    }
  }
 
}
</script>

<style scoped>
  .pozadina{
  
    width: 100%;
    min-height: 700px;
    
  }
  .login{
    background-color: #dfd7da;
    width: 30%;
    border-radius: 20px;
    margin: 5% auto;
    padding: 2% 0;
    font-family:'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
  }
  .naslov{
    border-bottom: 1.5px solid 	rgb(116, 108, 109);
    width: 80%;
    margin: auto;
    margin-bottom: 10%;
  }

  .eror{
    color: red;
  }

  form{
    font-size: 20px;
    width: 80%;
    margin: auto;
  }
  .form-group{
    margin: 6% 5%;
    clear: both;
  }
  input{
    border-radius: 12px;
    padding: 6% 4%;
  }
  form button{
    font-size: 20px;
    border-radius: 15px;
    width: 60%;
    margin:auto;
    background-color:rgb(77, 99, 114);
    border: none;
    padding: 3%;
    color: white;
    margin-top: 20px;
  }
   form button:hover{
     box-shadow: 9px 9px 7px gray;
    }

  @media(max-width: 600px){

   .login{
    width: 70%;
    border-radius: 20px;
    margin: 10% auto;
    padding: 2% 0;
    font-family:-apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
    background-color: #dfd7da;
  }



  

}

</style>

