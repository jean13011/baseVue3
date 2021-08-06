<template>
  <h3>Toutes les technos à veiller</h3>
  <ul>
    <!--pour chaque techno dans les technos je veux le nom de LA techno et la clé est l'id unique,
        on oublie pas de bien return la variable car on l'utilise-->
    Total: {{technos.length}}

    <li v-for="tech in technos" :key="tech.id">
      <button @click="deleteTech(tech)">X</button>
      <button @click="updateTech(tech)">modifier</button>
        <!--si la tech a editer est differente de null et on selection uniquement la ligne qui correspond a l'id de la tech que l'on veut modifier
        alors quand on entrera entrée on appellera save-->
      <span v-if="techToEdit !== null && techToEdit.id === tech.id">
        <input type="text" v-model="techToEdit.name" @keypress.enter="save">
        <button @click="save">Sauvegarder</button>
      </span>
      <span>
        {{tech.name}}
      </span>
    </li>

  </ul>
</template>

<script>
import {ref} from "vue";

export default {
  emits : ["deleteTech"],
  name: "TechnoList",
  props : {
    technos : {
      /*typage tableau et requis pour technos*/
      type : Array,
      required: true
    }
  },
  /*recuperation de la methode emit du context*/
  setup(props, {emit}){

    let techToEdit = ref(null);

    const deleteTech = function (tech) {
      emit("delete", tech);
    }

    const updateTech = function (tech){
      techToEdit.value = tech;
    }

    const save = function (){
      techToEdit.value = null;
    }

    return{
      deleteTech,
      updateTech,
      save,
      techToEdit
    }
  }
}
</script>

<style scoped>

</style>