<template>
    <div class="trazilica">
            <div class="row">
                <div class="form-group">
                    <h3><strong>Pretraži dadilju po gradu</strong></h3>  
                    <select v-model="searchterm" class="form-control form-control-lg">
                        <option :key="g.id" v-for="g in gradovi">{{g}}</option>
                    </select>
                    <button @click="search(searchterm)" class="btn btn primary" type="submit"><strong>Traži</strong></button>
                </div>
            </div>   
        <p v-if="brojac">Nema registriranih dadilja u tom gradu. Pokušajte u nekom drugom gradu.</p>
        <div style="margin-bottom: 80px">
        <Pretrazenprofil :key="pretrazi.id" :podatak="pretrazi" v-for="pretrazi in filteredCards"/>
        </div>
    </div>  
</template>


<script>
import store from '@/store.js'
import Pretrazenprofil from '@/components/Pretrazenprofil.vue'
export default {

    data(){
        return store;
    },
    name: 'Trazilica',
  components: {
    Pretrazenprofil
  },
  computed: {
   filteredCards () {
           
            return this.znj;   
   }
  },
  methods:{
    search(searchterm) {
      const self=this;
      db.collection("dadilja").where("grad", "==", searchterm)
        .onSnapshot(function(snapshot) {
          snapshot.docChanges().forEach(function(change) {
            const data = change.doc.data()
              if (change.type !== "added") return
              else {
                  self.brojac = false;
                  const pretrazen = {id: change.doc.id, ime: data.ime,prezime: data.prezime, spol:data.spol, brojgodina:data.brojgodina, grad:data.grad, kontakt:data.kontakt, ostalo:data.ostalo}
                  self.znj.unshift(pretrazen)
              }
          });
      });
      
      if(self.znj=[]){
          self.brojac=true;
      }
      self.znj = [];
        
    }
      

    }
  }

</script>

<style scoped>

    .trazilica {
      font-family:'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
    }

    h3 {
      margin-bottom: 10%;
    }

    .form-group{
    margin: auto;
    width: 30%;
    clear: both;
    text-align:center;
  }

  select{
    border-radius: 12px;
    width: 60%;
    float: left;  
  }
  .row{
    padding: 0;
    margin: 4% 5%;
}
button{
    width: 30%;
    border-radius: 10px;
    font-size: 20px;
    float: right;
    background-color:rgb(175, 196, 204);
    border: none;
    color: white;
}
 button:hover{
     box-shadow: 9px 9px 7px gray;
    }    
    
p{
  font-size: 20px;
}

 @media(max-width: 700px){

     h3 {
      margin-top: 5%; 
      margin-bottom: 15%;
    }

    .form-group{
    width: 70%;
  }

 }

</style>