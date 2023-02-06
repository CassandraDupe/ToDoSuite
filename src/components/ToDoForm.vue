<script setup>
import { ref } from "vue";
// -- donnée réactive pour la saisie du libellé
const libelle = ref("");
// -- les events émis par le composant
const emit = defineEmits(["addc"]);
// -- handler utile si on veut gérer le submit de cette manière
// <form @submit.prevent="handlerSubmit">
function handlerSubmit() {
  // en dehors du template il faut se souvenir que libelle
  // est un objet avec l'attribut value (créé par ref())
  emit("addc", libelle.value);
  libelle.value = "";
}
</script>

<template>
  <!-- quand le formulaire est validé,
    on doit emmetre un event vers le composant parent 
    pour faire ressortir du composant 
    la valeur de la variable "libelle";
  -->

  <form @submit.prevent="$emit('addc', libelle)">
    <!-- 2ème syntaxe possible avec un handler
  <form @submit.prevent="handlerSubmit">
  -->
    <!-- la direective v-model permet de faire le lien bidirectionnel
         entre la variable et la zone de saisie ;
         si on modifie la var, la zone de saisie est modifié
         si on modifie la zone de saisir, la variable est modifié
         -->
    <input type="text" v-model="libelle" placeholder="chose ?" />
    <input type="submit" value="valider" />
  </form>
</template>

<style scoped>
</style>
