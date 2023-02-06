<script setup>
// -- import de la fonction permettant de déclarer
//   une variable comme une varianel d'ETAT
import { reactive } from "vue";

// -- les 2 sous composants utilisés
import ToDoListItem from "./ToDoListItem.vue";
import ToDoForm from "./ToDoForm.vue";

// -- la classe Chose
import Chose from "../Chose";

// -- la liste des choses --> dans le state
// --> donnée réactive = l'affichage sera actualisée
//      automatiquement à chque cght dans la liste
const listeC = reactive([]);
const url = "https://webmmi.iut-tlse3.fr/~pecatte/todos/public/1/todos"; // l’url de la ressource

function getTodos() {
  const fetchOptions = { method: "GET" }; // les options de l'API fetch
  // executer la req AJAX
  fetch(url, fetchOptions)
    .then((response) => {
      return response.json();
    })
    .then((dataJSON) => {
      // dataJSON = les données renvoyées
      console.log(dataJSON); // ici le traitement des données …
      // pour affichage dans le navigateur
    })
    .catch((error) => console.log(error));
}

onMounted(() => {
  getTodos();
});

// -- handler pour 'faire/défaire' une chose à prtir de l'index dans la liste
function handlerFaire(idx) {
  listeC[idx].faire();
}
// -- handle pour supprimer une chose à prtir de l'index dans la liste
function handlerDelete(idx) {
  listeC.splice(idx, 1);
}
// -- handler pour ajouter une nouvelle chose à partir
//    du libelle saisi dans le formulaire
//     qui se retrouve en paramétre
function handlerAdd(libelle) {
  // -- il faut créer une nouvelle "chsoe" instance de la classe
  listeC.push(new Chose(libelle));
}
</script>

<template>
  <h3>Liste des choses à faire</h3>
  <!-- Utiliser le composant "todoform" pour saisir le texte de la chose 
       il faut écouter l'event "addc" émis par la composant pour prévenir
      que la saisie est terminée  -->
  <ToDoForm @addc="handlerAdd"></ToDoForm>
  <ul>
    <!-- 
      le composant todoitem sert à afficher une chose ;
      en paramètre d'entrée, il a besoin de 2 elts appelés "props"
         - la chose à afficher et l'index dans le tableau listeC
      il comporte 2 boutons pour faire / supprimer
      il emet un event quand le bouton est cliqué
        "deletec" pour la supression, "fairec" pour faire/défaire
    -->
    <ToDoListItem
      v-for="(chose, index) of listeC"
      :key="chose.id"
      :chose="chose"
      :indexc="index"
      @deletec="handlerDelete"
      @fairec="handlerFaire"
    />

    <!-- afficher la liste sans le composant "todolistitem"
    <li v-for="(chose, index) of listeC" :key="chose.id">
      {{ chose.pourAfficher() }}
      <button @click="handlerDelete(index)">Supprimer</button>
      <button @click="handlerFaire(index)">Faire</button>
    </li>
    -->
  </ul>
</template>

<style scoped>
</style>
