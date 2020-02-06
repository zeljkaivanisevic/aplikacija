<template>
  <div class="home">
    <div> 
      <div><img class="naslovna" style="max-height: 600px;" src="novo.jpg" alt="dadilja i dijete"> </div>
        <div>
          <div class="tekst">
            <h1><strong>Dobrodošli u aplikaciju <span style="color:#f77299;">Pronađi dadilju.</span></strong></h1>
            <h4> Aplikacija je namjenjena roditeljima koji traže dadilju te dadiljama koje traže posao.
            Ako ste zainteresirani za jedno ili drugo ovo je pravo mjesto za vas.</h4>
            <router-link to="/Prijava"><button class="btn btn primary"><strong>Prijava</strong></button></router-link>
            <router-link to="/Registracija"><button class="btn btn primary"><strong>Registracija</strong></button></router-link>
          </div>
        </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src

export default {
  name: 'Home'
}
</script>
 
<style scoped>
   
   .home {
      background-color:#dfd7da;
      font-family:'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
   }
   button{
     margin: 8%;
     font-size: 30px; 
     border: none;
     border-radius: 20px;
     padding: 1.5% 6%;
     background-color:rgb(197, 160, 165);
     color: white; 
   }
    button:hover{
     box-shadow: 9px 9px 7px gray;
    }
  .tekst{
    width: 70%;
    margin: auto;

  }

  .tekst h1{
    margin: 5% 0% 5% 0%;
  }
  .tekst h4{
    line-height: 150%;

  }
  .naslovna{ 
    width: 100%;
    align-items: center;
  

  }

  @media(max-width: 600px){
  
    
     button{
     margin: 4px;
     width: 40%;
     border-radius: 20px;
     padding: 1% 5%;
     background-color:rgb(197, 160, 165);
     font-size: 150%;
     margin: 5%;
   }
    button:hover{
     box-shadow: 9px 9px 7px gray;
    

    }
  .tekst{
    width: 80%;
    margin: auto;
  }

  .tekst h1{
    margin-bottom: 5%;
    font-size: 35px;
    margin-top: 10%;
  }
  .tekst h4{
    line-height: 150%;
    font-size: 130%;

  }
  
  .row{
    margin: auto;
  }
  
  .naslovna{ 
    width: 100%;
    align-items: center;

   

 
  }


  }
</style>