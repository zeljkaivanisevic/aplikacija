<template>
    <div class="naslovna">
      <div v-if="authenticated">
        <form @submit.prevent="Objavi">
            <div class="form-group">
                <div class="kreirajteobjavu">
                    <strong><p>Kreirajte objavu</p></strong>
                </div>
                 <input v-model="naslov" class="naslov" type="text"  placeholder="Unesite naslov">
                <textarea v-model="novaobjava"  type="text" placeholder="Dodajte objavu..." style="font-size: 80%;"></textarea>
            </div>
              <button class="btn btn primary" type="submit"><strong>Objavi</strong></button>
        </form>
        </div>
        <div style="margin-bottom: 70px">
        <Objava :key="karla.id" :info="karla" v-for="karla in filteredCards" />
        </div>
    </div>

    
</template>

<script>
    
    import Objava from '@/components/Objava.vue'
    import store from '@/store.js'

export default {
    data(){
        return store;
    },
  name: 'Naslovna',
  components: {
    Objava
  },
  computed: {
   filteredCards () {
    return this.postovi;
   }
  },


  methods: {
    Objavi(){
         db.collection("objave").add({        
          tekst: this.novaobjava,
          ime: this.ime,
          prezime: this.prezime,
          naslov: this.naslov,
          posted_at: Date.now()
        })
        this.naslov='';
        this.novaobjava='';
    }
  },
  mounted(){
    db.collection("objave").orderBy("posted_at")
      .onSnapshot(snapshot => {
        snapshot.docChanges().forEach(change => {
          const data = change.doc.data()
          if (change.type !== "added") return
            const karla = {tekst: data.tekst, ime: data.ime,prezime: data.prezime, naslov: data.naslov, posted_at: data.posted_at}
            this.postovi.unshift(karla)
        });
    });
  }

    
}
</script>

<style scoped>

p {
    margin: 0 5%;
    padding: 2% 0;
}
  
  form{
    font-size: 20px;
    width: 30%;
    margin: auto;
    margin-top: 2%;
    margin-bottom: 5%;
    font-family:'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
  }


.form-group{
    clear: both;
    text-align: left;
    margin-bottom: 5px;
    border-style:ridge;
}

.kreirajteobjavu{
    background: rgb(175, 196, 204);
    font-size: 20px;
    color: white;
    
}

textarea{
  font-size: 20px; 
  width: 100%;
  font-family: Cambria, Cochin, Georgia, Times, 'Times New Roman', serif;
  border: none;
  margin: 0;
}

button{
     float: center;
     font-family: Cambria, Cochin, Georgia, Times, 'Times New Roman', serif;
     background-color:rgb(175, 196, 204);
     width: 40%;
     font-size: 20px;
     color: white;
     border-radius: 15px;
    }

  button:hover{
    box-shadow: 9px 9px 7px gray;
    }    
    

.naslov{
  width: 100%;
  font-size: 80%;
  font-family: Cambria, Cochin, Georgia, Times, 'Times New Roman', serif;
  padding: 1.5%;

  
}

@media(max-width: 700px){

  form{
    width: 60%;
    margin-top: 5%;
    margin-bottom: 5%;
  }

  .form-group{
    margin-bottom: 8px;
   
}

button{
     float: center;
     font-family: Cambria, Cochin, Georgia, Times, 'Times New Roman', serif;
     background-color:rgb(175, 196, 204);
     width: 50%;
     font-size: 20px;

    }




}



</style>