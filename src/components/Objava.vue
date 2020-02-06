<template>
    <div class="card text-center" id="card">
        <div class="card-header text-left" style="background-color: white;">
         <strong>{{ info.ime }} {{info.prezime}}</strong>
        </div> 
        <div class="card-header text-left" style="color: white;">
          <strong>{{info.naslov}}</strong>
        </div>
        <div class="card-body" style="background-color: white;">
          
          {{info.tekst}}
          
        </div>
        <div class="card-footer text-left" style="color: white;">
          <strong>Posted: {{timeAgo}} </strong>
        </div>
    </div>
</template>

<script>
import moment from 'moment'
import store from '@/store.js'
export default {
    props: ["info"],
    data () {
     return store;
  },
  
  computed: {
    timeAgo () {
      return moment(this.info.posted_at).fromNow()
    }
  },

}
</script>

<style scoped>

  #card{
    margin: auto; 
    width: 30%; 
    margin-bottom: 30px;
    background: rgb(175, 196, 204);
    font-size: 18px;
    font-family:'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
  }


@media(max-width: 700px){
  #card{
    width: 60%; 
    font-size: 15px;
  }
}

</style>
