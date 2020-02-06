<template>
  <div id="app">
    <div id="nav">


      <header>

        
			<!--Navbar-->
        <div class="contejner">

          <!-- Brand/logo -->
          <div class="pronadi">
            <router-link to="/" v-if="!authenticated"><h1><strong>Pronađi <span class="dadilju">dadilju</span></strong></h1></router-link>
            <router-link to="/Naslovna" v-if="authenticated"><h1><strong>Pronađi <span class="dadilju">dadilju</span></strong></h1></router-link>
          </div>

          <nav>
      
            <!-- Links -->
          
            <ul>
              <li><router-link v-if="!authenticated" to="/"><img id="home" src="home.png">Početna</router-link></li>
              <li><router-link v-if="!authenticated" to="/Prijava"><img id="login" src="login.png">Prijava</router-link></li>
              <li><router-link v-if="!authenticated" to="/Registracija"><img id="registration" src="registration.png">Registracija</router-link></li>
              <li><router-link v-if="!authenticated"  to="/About"><img id="about" src="about.png">O nama</router-link></li>
              <li><router-link v-if="authenticated" to="/Naslovna"><img id="home" src="home.png">Naslovna</router-link></li>
              <li><router-link v-if="authenticated" to="/mojprofil"><img id="profil" src="user-profile.png">Moj profil</router-link></li>
              <li><router-link v-if="authenticated" to="/Trazilica"><img id="search" src="search.png">Tražilica</router-link></li>
              <li><router-link v-if="authenticated" to="/Postavke"><img id="postavke" src="postavke.png">Promjena lozinke</router-link></li>
              <li v-if="authenticated">
                <a @click.prevent="logout" href="#"><img id="logout" src="logout.png">Odjava</a>
              </li>
            </ul>

          </nav>

        </div>
        <!--Kraj Navbar-a-->

		</header>

    <div class="crta"></div> 
    </div>
    <router-view/>
    <footer>
			<div id="footer">	
				<div class="container">
				<p style="padding-top: 10px;"><strong>Aplikacija <span class="bottom"> Pronađi dadilju 2020</span></strong></p>	
				</div>
			</div>
		</footer>
  </div>
</template>

<script>
import store from '@/store.js'
export default {
  data (){
    return store;
  },

  methods: {
    logout() {
      firebase.auth().signOut();
    }
  },
  
  mounted() {
    const self = this;
    firebase.auth().onAuthStateChanged(function(user) {
      if (user) {
        self.userEmail = user.email;
        self.authenticated = true;

        db.collection("roditelj")
        .doc(self.userEmail)
        .get()
        .then(doc => {
          if (doc.exists) {
            console.log("Document data:", doc.data());
            self.ime = doc.data().ime;
            self.prezime = doc.data().prezime;
            self.kontakt = doc.data().kontakt;
            self.brojdjece = doc.data().broj;
            self.tip = doc.data().tip;
            self.grad = doc.data().grad;
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
            self.ime = doc.data().ime;
            self.prezime = doc.data().prezime;
            self.kontakt = doc.data().kontakt;
            self.grad = doc.data().grad;
            self.tip = doc.data().tip;
            self.iskustvo = doc.data().iskustvo;
            self.ostalo = doc.data().ostalo;
            self.brojgodina = doc.data().brojgodina;
            self.mjestocuvanjadjece = doc.data().mjestocuvanjadjece;
            self.spol = doc.data().spol;
            self.dozvola = doc.data().dozvola;

          } else {
            // doc.data() will be undefined in this case
            console.log("No such document!");
          }
        });
        
        console.log(`Authenticated: ${self.userEmail}`)
        if (self.$route.name !== 'Naslovna')
          self.$router.push({name: 'Naslovna'})
      }
      else {
        self.authenticated = false
        console.log('Logged out')
        if (self.$route.name !== 'Home')
          self.$router.push({name: 'Home'})
      }
    });
    }
  
}
</script>

<style lang="scss">

  #home{
  margin-right: 10px;
  height: 30px;
  width: 30px;
}
  #login{
  margin-right: 10px;
  height: 30px;
  width: 30px;
}
 #registration{
  margin-right: 10px;
  height: 30px;
  width: 30px;
}
 #profil{
  margin-right: 10px;
  height: 30px;
  width: 30px;
}
#search{
  margin-right: 10px;
  height: 30px;
  width: 30px;
}

 #about{
  margin-right: 10px;
  height: 30px;
  width: 30px;
}
#logout{
  margin-right: 10px;
  height: 30px;
  width: 30px;
}
#postavke{
  margin-right: 10px;
  height: 30px;
  width: 30px;
}
.contejner{
	width: 90%;
	margin: auto;
	overflow: hidden;
	position: relative;
}
header{
  background:#b7c0c7;
	margin: 0;
	min-height: 70px;
  width: 100%;

}

.dadilju{
  color: rgb(116, 108, 109);
}

.crta{
	background:rgb(116, 108, 109);
	height: 4px;
	width: 100%;
}

.pronadi{
  float: left;
	margin: 12px 0;
  font-family:'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
}

nav{
  margin-top: 20px;
}

nav ul{
	float: right;
	padding: 0;
  margin: 0;
  font-family:'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
}


nav ul li {
	padding: 0 15px;
  display: inline;
	font-size: 25px;
}

#footer {
  position: fixed;
  left: 0;
  bottom: 0;
  width: 100%;


	padding: 0.2%;
	color: white;
	background-color: #b7c0c7; 
	text-align: center;
	font-size: 18px;
  font-family:'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
}

.bottom{
  color: rgb(116, 108, 109);
}


#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;

}
 
#nav {
  

  a{
    font-weight: bold;
    color: white;
    text-decoration: none;

    &.router-link-exact-active {
      color: white;
    }
  }
}

@media(max-width: 700px){

#nav h2{
  margin: auto;
}

nav ul {
	margin: auto;  
  
}

nav ul li{
	font-size: 18px;
	padding: 5px 6px;

}

}
</style>
