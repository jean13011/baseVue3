<template>
  <h1>Veille techno</h1>
  <!--  recupération de l'émission du contexte add de l'enfant et appel de save-->
  <Form @add="save" />
  <br>
  <!--bind de la props technos -->
  <TechnoList  :technos="technos" @delete="deleteTech" />

</template>

<script>

import Form from "./components/Form";
import TechnoList from "./components/TechnoList";

import {ref} from "vue";
export default {
  name: 'App',
  components: {
    Form,
    TechnoList,
  },

  setup(){
    /*variable technos = tableau d'objet reactif avec ref()*/
    let  technos = ref([]);

    const save = function(data) {
      /*[...] Syntaxe de décomposition */
      technos.value = [...technos.value, { name : data, id : Date.now()}]
    }

    const deleteTech = function(tech){
      technos.value = technos.value.filter(t => t.id !== tech.id);
    }

    return{
      save,
      technos,
      deleteTech,
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

ul{
  list-style: none;
}
</style>
