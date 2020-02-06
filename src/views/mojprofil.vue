<template>
    <div class="profil">
        <div class="row">
		  <div class="naslov" >
		      <h2><strong>Moj profil</strong></h2>
              <router-link to="/Urediprofil"><button class="btn btn primary"><strong><img id="edit" src="edit.png">Uredi</strong></button></router-link>
          </div>
		</div>
        <br>

    <div class="roditelj" v-if="tip==='roditelj'" >
      <div class="col-md-10" style="margin:auto;">
          <div class="form-group row" >
            <label for="username" class="col-6"><strong>Ime</strong></label>
            <div class="col-6">
                {{ime}}
            </div>
          </div>
          <div class="form-group row">
            <label for="name" class="col-6"><strong>Prezime</strong></label>
            <div class="col-6">
                {{prezime}}
            </div>
          </div>
          <div class="form-group row">
            <label for="lastname" class="col-6"><strong>Grad</strong></label>
            <div class="col-6">
              {{grad}}
            </div>
          </div>
          <div class="form-group row">
            <label for="text" class="col-6"><strong>Kontakt broj</strong></label>
            <div class="col-6">
              {{kontakt}}
            </div>
          </div>
          <div class="form-group row">
            <label for="email" class="col-6"><strong>Broj djece</strong></label> 
            <div class="col-6">
              {{brojdjece}}
            </div>
          </div>
      </div>
    </div>  


    <div class="dadilja" v-if="tip==='dadilja'" >
        <div class="col-md-10" style="margin:auto;">
                <div class="form-group row">
                    <label for="username" class="col-6"><strong>Ime</strong></label> 
                    <div class="col-6">
                    {{ime}}
                    </div>
                </div>
                    <div class="form-group row">
                    <label for="name" class="col-6"><strong>Prezime</strong></label> 
                    <div class="col-6">
                        {{prezime}}
                    </div>
                </div>
                <div class="form-group row">
                    <label for="text" class="col-6"><strong>Koliko imam godina</strong></label> 
                    <div class="col-6">
                       {{brojgodina}}
                    </div>
                </div>
                <div class="form-group row">
                    <label for="name" class="col-6"><strong>Spol</strong></label> 
                    <div class="col-6">
                        {{spol}}
                    </div> 
                    </div>
                <div class="form-group row">
                    <label for="lastname" class="col-6"><strong>Grad</strong></label> 
                    <div class="col-6">
                        {{grad}}
                    </div>
                </div>
                <div class="form-group row">
                    <label for="select" class="col-6"><strong>Kontakt broj</strong></label>
                    <div class="col-6">
                        {{kontakt}}
                    </div>
                </div>
                <div class="form-group row">
                    <label for="email" class="col-6"><strong>Godine iskustva</strong></label>
                    <div class="col-6">
                        {{iskustvo}} god
                    </div>
                </div>
                <div class="form-group row">
                    <label for="email" class="col-6"><strong>Vozačka dozvola</strong></label>
                    <div class="col-6">
                        {{dozvola}}
                    </div>
                </div>
                <div class="form-group row">
                    <label for="email" class="col-6"><strong>Mjesto čuvanja djece</strong></label> 
                    <div class="col-6">
                        {{mjestocuvanjadjece}} 
                    </div>
                </div>
                <div class="form-group row">
                    <label for="email" class="col-6"><strong>Ostalo</strong></label> 
                    <p style="white-space: pre-line; font-size: 80%;"></p>
                    <br>
                    <div class="col-6">
                        {{ostalo}}
                    </div>
                </div>
        </div>
    </div>
        
    
    </div>
</template>

<script>
import store from '@/store.js'
export default {
    data () {
     return store;
    },

}
</script>

<style scoped>

     #edit{
        margin-right: 10px;
        height: 30px;
        width: 30px;
    }
    .profil{
        margin: 5% auto; 
        font-size: 20px;
        width: 40%;
        background-color: #dfd7da;
        border-radius: 20px;
        padding: 2% 0;
        font-family:'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
    }
    
    h2{
        float: left;
    }

    button {
        float: right;
         border-radius: 10px;
         width: 30%;
         font-size: 20px;
         background-color:rgb(77, 99, 114);
         border: none;
         padding: 5px 0;
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
        font-size: 20px; 
        width: 100%;
        font-family:-apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
    }


     @media(max-width: 700px){

        .profil{
        margin: 8% auto; 
        width: 80%;
        padding: 5% 0;
    }

    button {
   
         width: 40%;
         padding: 5px 0;
    
        }

    }


 
</style>