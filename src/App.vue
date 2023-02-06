<script setup>
// ==> ne pas oublier "setup" pour l'API composition
// -- importer les composants utilisés
import ToDoHeader from "./components/ToDoHeader.vue";
import ToDoList from "./components/ToDoList.vue";
</script>

<template>
  <!-- utilisation des 2 composants -->
  <ToDoHeader />
  <ToDoList />
</template>

<style>
</style>
