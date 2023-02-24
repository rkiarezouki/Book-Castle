<script setup>
import { ref } from "vue";
const titre = ref("");
const prix = ref(0);
const qte = ref(0);
const emit = defineEmits(["addLivre"],["chercherLivre"]);


</script> 


<template>

  <form @submit.prevent="$emit('addLivre', {titre: titre, qtestock: qte, prix:prix})">
    <input type="text" v-model="titre" placeholder="Ajouter un titre" />
    <input type="text" v-model="prix" placeholder="Ajouter le prix" />
    <input type="text" v-model="qte" placeholder=" La quantité" />
    <input id="Test" type="submit" value="Ajouter" />
</form>




  <h1></h1>
</template>

<style scoped>

form{
   font-size: 40px; 
  text-align: center;
  padding:5px; 
   border:0; 
  
  box-shadow:0 0 15px 4px rgba(0,0,0,0.06); 
}
input#Test{
   background-color: #A0B2D6; 
   font-family: 'MagicSchoolOne';
}
@font-face {
  font-family: 'MagicSchoolOne';
  src: url('/public/MagicSchoolOne.ttf');
}
</style>