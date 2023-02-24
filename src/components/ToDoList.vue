<script setup>
// const books = ref([]);
import { reactive, onMounted } from "vue";
import ToDoListItem from "./ToDoListItem.vue";
import ToDoForm from "./ToDoForm.vue";
import Livre from "../Livre.js";
import { ref } from "vue";



const listelivre = reactive([]);
// -- l'url de l'API
const url = "https://webmmi.iut-tlse3.fr/~pecatte/librairies/public/32/livres";
function getTodos() {
  const fetchOptions = { method: "GET" };
  fetch(url, fetchOptions)
    .then((response) => {
      return response.json();
    })
    .then((dataJSON) => {
      console.log(dataJSON);
      // -- vider la liste des choses
      listelivre.splice(0, listelivre.length);
      // pour chaque donnée renvoyée par l'API
      //  créer un objet instance de la classe Chose
      //  et l'ajouter dans la liste listelivre
      dataJSON.forEach((liv) =>
        listelivre.push(new Livre(liv.id, liv.titre, liv.qtestock,liv.prix ))
      );
    })
    .catch((error) => console.log(error));
}
onMounted(() => {
  getTodos();
});

function handlerAdd(livre) {
  console.log(livre, JSON.stringify(livre));
  let myHeaders = new Headers();
  myHeaders.append("Content-Type", "application/json");
  // --  le libelle de la nouvelle chose est envoyé au serveur
  //  via le body de la req AJAX
  const fetchOptions = {
    method: "POST",
    headers: myHeaders,
    body: JSON.stringify({titre :livre.titre ,qtestock: livre.qtestock, prix: livre.prix})
  };
  fetch(url, fetchOptions)
    .then((response) => {
      return response.json();
    })
    .then((dataJSON) => {
      console.log(dataJSON);
      getTodos();
    })
    .catch((error) => console.log(error));
}




function handlerDelete(id) {
  console.log(id);
  const fetchOptions = {
    method: "DELETE",
  };
  // -- l'id de la chose à supprimer doit être
  //  ajouté à la fin de l'url
  fetch(url + "/" + id, fetchOptions)
    .then((response) => {
      return response.json();
    })
    .then((dataJSON) => {
      console.log(dataJSON);
      getTodos();
    })
    .catch((error) => console.log(error));
}

const mottest = ref("");

function handlerSearch(mottest) {
  console.log("quesque tu m'affiche ici", mottest);
  const fetchOptions = {
    method: "GET",
  };
  // -- l'id de la chose à supprimer doit être
  //  ajouté à la fin de l'url
  fetch(url + "?search=" + mottest, fetchOptions)
    .then((response) => {
      return response.json();
    })
    .then((dataJSON) => {
      console.log("Mes livre dans la fonction search", dataJSON);
     listelivre.splice(0, listelivre.length);
      // pour chaque donnée renvoyée par l'API
      //  créer un objet instance de la classe Chose
      //  et l'ajouter dans la liste listelivre
      dataJSON.forEach((liv) =>
        listelivre.push(new Livre(liv.id, liv.titre, liv.qtestock,liv.prix )))})
   
    
    .catch((error) => console.log(error));

}




function handlerDecrement(livre) {


  console.log(livre);
  // -- faire la chose
  livre.Todecrement();

  (livre.qtestock <= 0?handlerDelete(livre.id):Decrement )

  const Decrement=()=>{
    // -- entête http pour la req AJAX
  let myHeaders = new Headers();
  myHeaders.append("Content-Type", "application/json");
  // -- la chose modifiée est envoyé au serveur
  //  via le body de la req AJAX
  const fetchOptions = {
    method: "PUT",
    headers: myHeaders,
    body: JSON.stringify({id :livre.id,titre :livre.titre ,qtestock: livre.qtestock, prix: livre.prix}),
  };
  // -- la req AJAX
  fetch(url, fetchOptions)
    .then((response) => {
      return response.json();
    })
    .then((dataJSON) => {
      console.log(dataJSON);
      // actualiser la liste des choses
      getTodos();
    })
    .catch((error) => console.log(error));
  }
  
}

function handlerIncrement(livre) {
  console.log(livre);
  // -- faire la chose
  livre.Toincrement();
  // -- entête http pour la req AJAX
  let myHeaders = new Headers();
  myHeaders.append("Content-Type", "application/json");
  // -- la chose modifiée est envoyé au serveur
  //  via le body de la req AJAX
  const fetchOptions = {
    method: "PUT",
    headers: myHeaders,
    body: JSON.stringify({id :livre.id,titre :livre.titre ,qtestock: livre.qtestock, prix: livre.prix}),
  };
  // -- la req AJAX
  fetch(url, fetchOptions)
    .then((response) => {
      return response.json();
    })
    .then((dataJSON) => {
      console.log(dataJSON);
      // actualiser la liste des choses
      getTodos();
    })
    .catch((error) => console.log(error));
}

</script>
<template>
  <h3>Mes livres</h3>
  <div>
    <input type="text" ref="mottest"   placeholder="Rechercher un titre" />
  <button @click="handlerSearch(mottest.value)" >OK</button>
</div>

  

  <ToDoForm @addLivre="handlerAdd"></ToDoForm>

  <ul id="B1">
    <ToDoListItem v-for="livre of listelivre" :key="livre.id" :livre="livre" @deleteL="handlerDelete" @decrementL ="handlerDecrement" @incrementL="handlerIncrement"/>
    
  </ul>
</template>

<style scoped>

ul#B1{
  display: grid;
  grid-template-columns: repeat(4,1fr);
   grid-auto-rows: 0.25fr; 
  margin: auto;
  
}
h3 {

  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  color: #8F604E;
  border: 1px solid black;
  text-align: center;
  position: relative;
  font-size: 30px;
  font-family: 'MagicSchoolOne';

}

button{
  font-size: 10px;
  text-align: center;
  padding:10px;
  border:2px solid;
  background-color: #A0B2D6;
  box-shadow:0 0 15px 4px rgba(0,0,0,0.06);
  font-family: 'MagicSchoolOne';
 
 
}
 div{
  margin: 0 40%;
  font-family: 'MagicSchoolOne';
} 
@font-face {
  font-family: 'MagicSchoolOne';
  src: url('/public/MagicSchoolOne.ttf');
}
</style>