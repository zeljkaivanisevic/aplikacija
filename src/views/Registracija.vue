<template>
  <div class="registracija">
    
    <div class="naslov">
      <h1>Registracija</h1>
    </div>
    <button class="btn btn primary" v-on:click="prikazr"><strong>Registriraj se kao roditelj</strong></button>
    <button class="btn btn primary" v-on:click="prikazd"><strong>Registriraj se kao dadilja</strong></button>
    <div class="roditelj" v-if="prikazregistracijer">
      <form @submit.prevent="signupr">
        <div class="row">
          
            <input v-model="ime" type="ime" class="form-control" aria-describedby="emailHelp" placeholder="Ime" style="margin-right: 2.5%;">
            <input v-model="prezime" type="prezime" class="form-control" id="exampleInputEmail desna" aria-describedby="emailHelp" placeholder="Prezime" style="margin-left: 2.5%;">
        </div> 
        <div class="form-group">
            <input v-model="email" type="email" class="form-control" aria-describedby="emailHelp" placeholder="Unesi email">      
        </div>
        <div class="form-group">
            <input v-model="lozinka" type="password" class="form-control" placeholder="Lozinka">
        </div>
        <div class="form-group">
            <input v-model="potvrdalozinke" type="password" class="form-control" placeholder="Potvrdi lozinku">
        </div>
        <div class="form-group">
          <label style="font-size: 80%" for="spol">Grad</label> 
          <select v-model="grad" class="form-control form-control-lg">
            <option :key="g.id" v-for="g in gradovi">{{g}}</option>
          </select>
        </div>
        <div class="form-group">
            <input v-model="kontakt" id="text" placeholder="Kontakt broj" class="form-control" type="text">
        </div>
        <div class="form-group">
          <label style="font-size: 80%" for="brojdjece">Koliko imate djece</label>
            <select v-model="broj" class="form-control form-control-lg">
              <option :key="k.id" v-for="k in brojdjece">{{k}}</option>
            </select>
          </div>
          <button type="submit" class="btn btn primary"><strong>Registriraj se</strong></button>
      </form>

    </div>



    <div class="dadilja" v-if="prikazregistracijed">

      <form @submit.prevent="signupd">
          <div class="row">
          
            <input v-model="ime" type="name" class="form-control" aria-describedby="emailHelp" placeholder="Ime" style="margin-right: 2.5%;">
            <input v-model="prezime" type="lastname" class="form-control" id="exampleInputEmail desna" aria-describedby="emailHelp" placeholder="Prezime" style="margin-left: 2.5%;">
        </div> 
        <div class="form-group">
            <input v-model="email" type="email" class="form-control" aria-describedby="emailHelp" placeholder="Unesi email">      
        </div>
        <div class="form-group"> 
            <input v-model="lozinka" type="password" class="form-control" placeholder="Lozinka">
        </div>
        <div class="form-group"> 
            <input v-model="potvrdalozinke" type="password" class="form-control" placeholder="Potvrdi lozinku">
        </div>
        <div class="form-group">
          <label style="font-size: 80%" for="spol">Spol</label> 
          <select v-model="a" class="form-control form-control-lg">
            <option :key="s.id" v-for="s in spol">{{s}}</option>
          </select>
        </div>
        <div class="form-group">
          <label style="font-size: 80%" for="spol">Grad</label> 
          <select v-model="grad" class="form-control form-control-lg">
            <option :key="g.id" v-for="g in gradovi"><p>{{g}}</p></option>
          </select>
        </div>
        <div class="form-group">
          <input v-model="brojgodina"  min=18 max=60 placeholder="Koliko imate godina?" class="form-control here" required="required" type="number">
        </div>
        <div class="form-group">
          <input v-model="kontakt"  name="text" placeholder="Kontakt broj" class="form-control here" required="required">
        </div>
        <div class="form-group">
          <label style="font-size: 80%" for="vozacka dozvola">Vozačka dozvola</label> 
          <select v-model="dozvola" class="form-control form-control-lg">
            <option :key="v.id" v-for="v in vozackadozvola">{{v}}</option>
          </select>
        </div>
        <div class="form-group">
          <label for="mjesto_cuvanja_djece" style="font-size: 80%">Mjesto čuvanja djece</label> 
           <select v-model="b" class="form-control form-control-lg">
            <option :key="m.id" v-for="m in mjestocuvanjadjece">{{m}}</option>
          </select>
          
        </div>
        <div class="form-group">
          <input v-model="iskustvo" id="iskustvo"  placeholder="Godine iskustva u radu s djecom" class="form-control here" type="text">
        </div>
        <div class="form-group">
          <p style="white-space: pre-line; font-size: 80%;"></p>
          <br>
          <textarea v-model="ostalo" placeholder="Ostalo" style="font-size: 80%;"></textarea>
        </div>
         <button type="submit" class="btn btn primary"><strong>Registriraj se</strong></button>
      </form>
    </div>

  </div>
</template>
<script>

export default {
  data (){
    return{
      ime :'',
      prezime:'',
      email:'',
      lozinka:'',
      potvrdalozinke:'',
      prikazregistracijer: false,
      prikazregistracijed: false,
      kontakt:'',
      brojdjece:["1", "2", "3", "4", "4+"],
      broj:'',
      grad: '',
      brojgodina:'',
      iskustvo: '',
      ostalo:'',
      mjestocuvanjadjece: ["Kod roditelja", "Kod dadilje", "Kod roditelja i kod dadilje"],
      b: '',
      spol:["muško", "žensko"],
      a:'',
      vozackadozvola:["Da", "Ne"],
      dozvola:'',
      gradovi:['Zagreb', 'Krapina', 'Sisak','Karlovac', 'Varaždin','Koprivnica','Bjelovar', 'Rijeka', 'Gospić', 'Virovitica', 'Požega', 'Slavonski Brod', 'Zadar','Osijek', 'Šibenik', 'Vukovar','Split','Pazin','Dubrovnik', 'Čakovec', 'Pula', 'Vinkovci']
    }
  },
  methods: {
    signupd () {
      let id= this.email;
      if (this.lozinka != this.potvrdalozinke) {
        alert (" Lozinke nisu točne. Pokušajte ponovo.")
          return;
      }
      firebase.auth().createUserWithEmailAndPassword(this.email, this.lozinka).then(() => {
        $('#login').modal('hide')


        db.collection("dadilja").doc(id).set({
          ime: this.ime,
          prezime: this.prezime,
          kontakt: this.kontakt,
          grad: this.grad,
          iskustvo: this.iskustvo,
          ostalo: this.ostalo,
          brojgodina: this.brojgodina,
          mjestocuvanjadjece: this.b,
          spol: this.a,
          dozvola: this.dozvola,
          tip:"dadilja"
          
        })
        .then(function(docRef) {
          console.log("Document written with ID: ", docRef.id);
        })
        .catch(function(error) {
          console.error("Error adding document: ", error);
        });
      })
    },


    signupr () {
      let id= this.email;
      if (this.lozinka != this.potvrdalozinke) {
        alert (" Lozinke nisu točne. Pokušajte ponovo.")
          return;
      }
      firebase.auth().createUserWithEmailAndPassword(this.email, this.lozinka).then(() => {
        $('#login').modal('hide')

        db.collection("roditelj").doc(id).set({
          ime: this.ime,
          prezime: this.prezime,
          grad: this.grad,
          kontakt: this.kontakt,
          broj: this.broj,
          tip:"roditelj"
        })
        .then(function(docRef) {
          console.log("Document written with ID: ", docRef.id);
        })
        .catch(function(error) {
          console.error("Error adding document: ", error);
        });
      })
    },


    prikazr(){
      this.prikazregistracijer=true
      if(this.prikazregistracijer==true){
        this.prikazregistracijed=false
      }
    },

    prikazd(){
      this.prikazregistracijed=true
      if(this.prikazregistracijed==true){
        this.prikazregistracijer=false
      }
    }
  }, 
}
</script>

<style scoped>
  .registracija{
    width: 35%;
    border-radius: 20px;
    margin: 5% auto;
    padding: 2% 0;
    font-family:'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
    background-color: #dfd7da;
  }
  .naslov{
    border-bottom: 1.5px solid 	rgb(116, 108, 109);
    width: 80%;
    margin: auto;
    margin-bottom: 5%;
  }

  form{
    font-size: 20px;
    width: 80%;
    margin: auto;
  }
  .form-group{
    margin: 4% 5%;
    clear: both;
    text-align: left;
  }
  input{
    border-radius: 12px;
    padding: 5.5% 4%;
  }
  select{
    border-radius: 12px;
    
  }
   button{
    font-size: 18px;
    border-radius: 15px;
    width: 45%;
    padding: 3%;
    margin:auto 2%;
    background-color:rgb(77, 99, 114);
    border: none;
    color: white; 
  }
  button:hover{
     box-shadow: 9px 9px 7px gray;
    }

.row{
    
    float: center;
    padding: 0;
    margin: 4% 5%;
}
.row input {
    width:47.5%;
}

textarea{
  font-size: 20px; 
  border-radius: 15px;
  width: 100%;
  font-family: Cambria, Cochin, Georgia, Times, 'Times New Roman', serif;
}

@media(max-width: 600px){

   .registracija{
    width: 80%;
    border-radius: 20px;
    margin: 10% auto;
    padding: 2% 0;
    font-family:-apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
    background-color: #dfd7da;
  }

  button{
    font-size: 15px;
    border-radius: 15px;
    width: 60%;
    padding: 5%;
    margin: 1%; 
  }

  input{
    border-radius: 12px;
    padding: 8% 4%;
  }

  .form-group{
    margin: 5% 5%;
  }

  form{
    font-size: 20px;
    width: 80%;
    margin: 3% auto auto auto;
  }

  

}

</style>

