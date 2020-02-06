<template>
    <div class="postavke">
      <div class="naslov">
        <h1>Promjena lozinke</h1>
      </div>
      <form @submit.prevent="promjenalozinke">
        <div class="form-group">
          <label> Postojeća lozinka</label>
          <input v-model="lozinka" type="password" class="form-control"  placeholder="Unesite postojeću lozinku">
        </div>
        <div class="form-group">
          <label> Nova lozinka</label>
          <input v-model="novalozinka" type="password" class="form-control"  placeholder="Unesite novu lozinku">
        </div>
        <div class="form-group">
          <label> Ponovite novu lozinku</label>
          <input v-model="potvrdalozinke" type="password" class="form-control" placeholder="Potvrdite novu lozinku">
        </div>  
        <button type="submit" class="btn btn primary"><strong>Spremi promjene</strong></button>
      </form>
    </div>
    
</template>
<script>
export default {
  data() {
    return {
      lozinka: '',
      
      novalozinka: '',
      potvrdalozinke:'',
  
    };
  },
  methods: {
    promjenalozinke() {
      if (this.novalozinka != this.potvrdalozinke) {
        alert (" Lozinke nisu točne. Pokušajte ponovo.")
          return;
      }
      var user = firebase.auth().currentUser;
      user.updatePassword(this.novalozinka).then(function() {
        })
        alert ("Lozinka je uspješno promjenjena.")
        if (this.$route.name !== "Naslovna")
              this.$router.push({ name: "Naslovna" })
            .catch(err => console.log(err))
            .catch(function(error) {
        });   
    }
  }
};
</script>

<style scoped>

  .postavke{
    background-color: #dfd7da;
    width: 30%;
    border-radius: 20px;
    margin: 3% auto 8% auto;
    padding: 2% 0;
    font-family:'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
  }

  .naslov{
    border-bottom: 1.5px solid 	rgb(116, 108, 109);
    width: 80%;
    margin: auto;
    margin-bottom: 8%;
  }
   input{
    border-radius: 12px;
    padding: 6% 4%;
  }
   form{
    font-size: 20px;
    width: 80%;
    margin: auto;
  }
  .form-group{
    margin: 8% 5%;
    clear: both;
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
  }
   form button:hover{
     box-shadow: 9px 9px 7px gray;
    }

  
      @media(max-width: 700px){

      .postavke{ 
      width: 70%;
      margin: 8% auto;
      padding: 4% 0;
    }

     input{
    padding: 8% 5%;
    }

    form button{
    width: 70%;
    }






      }


</style>