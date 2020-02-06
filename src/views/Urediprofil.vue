<template>
    <div class="profil">
        <div class="row">
		  <div class="naslov" >
		      <h2><strong>Uredi profil</strong></h2>
          </div>
		</div>
        <br>

    <div class="roditelj" v-if="tip==='roditelj'" >
      <form @submit.prevent="updater">
      <div class="col-md-10" style="margin:auto;">
          <div class="form-group row" >
            <label for="username" class="col-6"><strong>Ime</strong></label>
            <div class="col-6">
                <input v-model="ime" type="ime" class="form-control" aria-describedby="emailHelp" placeholder="Ime" style="margin-right: 2.5%;">
            </div>
          </div>
          <div class="form-group row">
            <label for="name" class="col-6"><strong>Prezime</strong></label>
            <div class="col-6">
               <input v-model="prezime" type="prezime" class="form-control" id="exampleInputEmail desna" aria-describedby="emailHelp" placeholder="Prezime" style="margin-left: 2.5%;">
            </div>
          </div>
          <div class="form-group row">
            <label for="lastname" class="col-6"><strong>Grad</strong></label>
            <div class="col-6">
              <select v-model="grad" class="form-control form-control-lg">
                <option :key="g.id" v-for="g in gradovi">{{g}}</option>
              </select>
            </div>
          </div>
          <div class="form-group row">
            <label for="text" class="col-6"><strong>Kontakt broj</strong></label>
            <div class="col-6">
              <input v-model="kontakt" id="text" placeholder="Kontakt broj" class="form-control" type="text">
            </div>
          </div>
          <div class="form-group row">
            <label for="email" class="col-6"><strong>Broj djece</strong></label> 
            <div class="col-6">
              <select v-model="broj" class="form-control form-control-lg">
                <option :key="k.id" v-for="k in brojdjece">{{k}}</option>
              </select>
            </div>
          </div>
      </div>
        <button type="submit" class="btn btn primary"><strong>Spremi</strong></button>
      </form>
    </div>  


            <div class="dadilja" v-if="tip==='dadilja'" >
              <form @submit.prevent="updated">
                <div class="col-md-10" style="margin:auto;">
                  <div class="form-group row">
                      <label for="username" class="col-6"><strong>Ime</strong></label> 
                      <div class="col-6">
                        <input v-model="ime" type="name" class="form-control" aria-describedby="emailHelp" placeholder="Ime" style="margin-right: 2.5%;">
                      </div>
                  </div>
                      <div class="form-group row">
                      <label for="name" class="col-6"><strong>Prezime</strong></label> 
                      <div class="col-6">
                          <input v-model="prezime" type="lastname" class="form-control" id="exampleInputEmail desna" aria-describedby="emailHelp" placeholder="Prezime" style="margin-left: 2.5%;">
                      </div>
                  </div>
                  <div class="form-group row">
                      <label for="text" class="col-6"><strong>Koliko imam godina</strong></label> 
                      <div class="col-6">
                        <input v-model="brojgodina"  min=18 max=60 placeholder="Koliko imate godina?" class="form-control here" required="required" type="number">
                      </div>
                  </div>
                  <div class="form-group row">
                      <label for="email" class="col-6"><strong>Spol</strong></label> 
                      <div class="col-6">
                          <select v-model="a" class="form-control form-control-lg">
                            <option :key="s.id" v-for="s in spol">{{s}}</option>
                          </select> 
                      </div>
                  </div>
                  <div class="form-group row">
                      <label for="lastname" class="col-6"><strong>Grad</strong></label> 
                      <div class="col-6">
                        <select v-model="grad" class="form-control form-control-lg">
                          <option :key="g.id" v-for="g in gradovi"><p>{{g}}</p></option>
                        </select> 
                      </div>
                  </div>
                  <div class="form-group row">
                      <label for="select" class="col-6"><strong>Kontakt broj</strong></label>
                      <div class="col-6">
                          <input v-model="kontakt"  name="text" placeholder="Kontakt broj" class="form-control here" required="required">
                      </div>
                  </div>
                  <div class="form-group row">
                      <label for="email" class="col-6"><strong>Godine iskustva</strong></label>
                      <div class="col-6">
                        <input v-model="iskustvo" id="iskustvo"  placeholder="Godine iskustva u radu s djecom" class="form-control here" type="text">
                      </div>
                  </div>
                  <div class="form-group row">
                      <label for="email" class="col-6"><strong>Vozačka dozvola</strong></label>
                      <div class="col-6">
                          <select v-model="dozvola" class="form-control form-control-lg">
                            <option :key="v.id" v-for="v in vozackadozvola">{{v}}</option>
                          </select>
                      </div>
                  </div>
                  <div class="form-group row">
                      <label for="email" class="col-6"><strong>Mjesto čuvanja djece</strong></label> 
                      <div class="col-6"> 
                          <select v-model="b" class="form-control form-control-lg">
                            <option :key="m.id" v-for="m in mjestocuvanjadjece">{{m}}</option>
                          </select> 
                      </div>
                  </div>
                  <div class="form-group row">
                      <label for="email" class="col-6"><strong>Ostalo</strong></label> 
                      <p style="white-space: pre-line; font-size: 80%;"></p>
                      <br>
                      <div class="col-6">
                        <p style="white-space: pre-line; font-size: 80%;"></p>
                        <br>
                        <textarea v-model="ostalo" placeholder="Ostalo" style="font-size: 80%;"></textarea> 
                      </div>
                  </div>
                </div>
                  <button type="submit" class="btn btn primary"><strong>Spremi</strong></button>
              </form>
            </div>
        
    
    </div>
</template>

<script>

export default {
    data () {
      return {
      ime: '',
      prezime: '',
      grad:'',
      gradovi: ['Bjelovar','Čakovec','Dubrovnik','Gospić','Karlovac','Koprivnica','Krapina','Osijek','Pazin','Požega','Pula','Rijeka', 'Sisak','Slavonski Brod','Split','Šibenik','Varaždin','Vinkovci','Virovitica','Vukovar', 'Zadar','Zagreb'],
      kontakt:'',
      broj:'',
      brojdjece:["1", "2", "3", "4", "4+"],
      brojgodina:'',
      a:'',
      spol:["muško", "žensko"],
      iskustvo:'',
      dozvola:'',
      vozackadozvola: ["Da", "Ne"],
      b:'',
      mjestocuvanjadjece: ["Kod roditelja", "Kod dadilje", "Kod roditelja i kod dadilje"],
      ostalo:'',
      tip:''
    }
  },

  created(){
     const self = this;
     var user = firebase.auth().currentUser;
      if (user) {
        self.userEmail = user.email;
        self.authenticated = true;

        db.collection("roditelj")
        .doc(self.userEmail)
        .get()
        .then(doc => {
          if (doc.exists) {
            console.log("Document data:", doc.data());
            self.tip = doc.data().tip;
          
          } else {
            // doc.data() will be undefined in this case
            console.log("No such document!");
          }
        });

        
        db.collection("dadilja")
        .doc(self.userEmail)
        .get()
        .then(doc => {
          if (doc.exists) {
            console.log("Document data:", doc.data());
            self.tip = doc.data().tip;
            

          } else {
            // doc.data() will be undefined in this case
            console.log("No such document!");
          }
        });
        
      }
        
  },

   methods: {
      updated() {
            var user = firebase.auth().currentUser;
            if (user) {
              db.collection("dadilja")
              .doc(this.userEmail)
              .update({ 
                ime: this.ime,
                prezime: this.prezime,
                grad: this.grad,
                kontakt: this.kontakt,
                spol: this.a,
                ostalo: this.ostalo,
                mjestocuvanjadjece: this.b,
                iskustvo: this.iskustvo,
                dozvola: this.dozvola,
                brojgodina: this.brojgodina
              })
              //.then(function() {
                console.log("Document successfully written!");
                alert("Uspješno ažuriran profil!");
                if (this.$route.name !== "mojprofil")
                  this.$router.push({ name: "mojprofil" }).catch(err => console.log(err))
              //})
            }else {
              //.catch(function(error) {
              console.error("Error writing document: ", error);
            //}),
            }    
        },

      updater() {
            var user = firebase.auth().currentUser;
            if (user) {
              db.collection("roditelj")
              .doc(this.userEmail)
              .update({ 
                ime: this.ime,
                prezime: this.prezime,
                grad: this.grad,
                kontakt: this.kontakt,
                broj: this.broj
              })
              //.then(function() {
                console.log("Document successfully written!");
                alert("Uspješno ažuriran profil!");
                if (this.$route.name !== "mojprofil")
                  this.$router.push({ name: "mojprofil" }).catch(err => console.log(err))
              //})
            }else {
              //.catch(function(error) {
              console.error("Error writing document: ", error);
            //}),
            }    
        } 
    }
  
}
</script>

<style scoped>


    .profil{
        margin: 5% auto; 
        font-size: 20px;
        width: 40%;
        background-color: #dfd7da;
        border-radius: 20px;
        padding: 2% 0;
        font-family:'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
    }
    input{
    border-radius: 12px;
    padding: 10%;
  }
  form{
    font-size: 20px;
    width: 100%;
    margin: auto;
  }
  .form-group{
    margin: 4% 3%;
    clear: both;
    text-align: left;
  }
  select{
    border-radius: 12px;
    
  }
    h2{
        float: left;
    }

    button {
        float: center;
         border-radius: 15px;
         width: 30%;
         font-size: 20px;
         background-color:rgb(77, 99, 114);
         border: none;
         padding: 9px 0;
         color: white;
        }

    button:hover{
     box-shadow: 9px 9px 7px gray;
    }    
    
    .naslov{
    border-bottom: 1.5px solid 	rgb(116, 108, 109);
    width: 80%;
    margin:auto;
    text-align: left;
    }

    textarea{
        border-radius: 15px;
        font-size: 20px; 
        width: 100%;
        font-family:-apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
    }

     @media(max-width: 700px){

       .profil{
        margin: 8% auto; 
        width: 80%;
      }

      input{
      padding: 13%;
    }

      button {
         width: 40%;
        }


     }
 
</style>
