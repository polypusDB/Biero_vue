<template>
  <div id="app" >
    <Header />
    <Dialog 
    :biere ="BiereAjouter"
    :ajouter = "ajouterBiere"
    :err = "erreur"/>
    <Dialog-mod 
    :biere = "biereModTesteur"
    :modifier="modifierBiere"/>
    <DialogSup 
    :effacer = "effacer"/>
    <b-container v-if="ListeBiere.length" class="bv-example-row">
    <b-row>
      <b-col sm='8' offset='2' v-if = "ListeBiere.length">
        <Bieres 
        v-for="biere in ListeBiere" 
        :biere="biere"
        :key = "biere.id_biere"
        :effacer="formModifier"
        :formModifier = "formModifier"/>
      </b-col>
    </b-row>
    </b-container>
  </div>
  
</template>

<script>
import Header from './components/Header.vue'
import Bieres from './components/Bieres.vue'
import Dialog from './components/Dialog.vue'
import DialogMod from './components/DialogModifier.vue'
import DialogSup from './components/DialogSup.vue'
import axios from "axios";


export default {
  name: 'App',
  components: {
    Header,
    Bieres,
    Dialog,
    DialogMod,
    DialogSup
  },
  data(){
    return{
      ListeBiere : [],
      auth : {},
      biereModTesteur : {},
      BiereAjouter:{},
      data: {},
      erreur : false
    }
  },
  methods:{
        effacer(){
          // console.log(this.biereModTesteur)
          let id = this.biereModTesteur.id_biere;
          axios.delete("http://127.0.0.1:8000/webservice/php/biere/" + id, this.auth
          ).then(()=>{
            this.getBiere();
          });
        },
        modifierBiere(id){
          this.dataSetteur(this.biereModTesteur);
          this.biereModTesteur = {};
          if(this.erreur){
            axios.post("http://127.0.0.1:8000/webservice/php/biere/" + id,this.data ,this.auth
            ).then(()=>{
              this.getBiere();
            });
          }
          else{
            this.getBiere();
          }

        },
        ajouterBiere(){
          this.dataSetteur(this.BiereAjouter);
          this.BiereAjouter = {};
          if(this.erreur){
            axios.put("http://127.0.0.1:8000/webservice/php/biere/",this.data ,this.auth
            ).then(()=>{
              this.getBiere();
            });
          }


        },
        getBiere(){

              fetch('http://127.0.0.1:8000/webservice/php/biere', {
                method : 'get'
              })
              .then((ListeBiere) =>{
                  return ListeBiere.json();
              })
              .then((jsonListeBiere) =>{
                this.ListeBiere = jsonListeBiere.data.reverse();
              })
        },
        formModifier(biere){
          console.log(biere);
          this.biereModTesteur = biere;
        },
        dataSetteur(biere){
          this.data.nom = biere.nom;
          this.data.brasserie = biere.brasserie;
          this.data.description = biere.description;
          this.data.image = biere.image;
          if(this.data.nom && this.data.brasserie && this.data.description && this.data.image){
            
            this.erreur = true;
          }
          else{
            this.erreur = false;
          }
        }

  },
  mounted: function(){
    this.getBiere();

    this.auth = {
                  auth : {
                          username : 'biero',
                          password : 'biero'
                          }
                }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
