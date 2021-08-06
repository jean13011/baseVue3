<template>
  <!--@submit.prevent = au submit la page ne se rafraichi pas-->
  <form @submit.prevent="add">
    <label for="techno">Techno à ajouter</label>
    <br>
    <!--v-model = liason du champs a une variable-->
    <input type="text" id="techno" v-model="tech">
    <br>
    <!--@click === v-on:click = au clic appel de fonction qui est dans la const add-->
    <button type="submit">Ajouter</button>
  </form>
</template>

<script>
import {ref} from "vue";

export default {
  /*pour emmètre custom event de l'enfant vers parent = context */
  /*pour emmètre custom event du parent vers enfant = props */
  setup(props, ctx) {
    //ref = reactive value
    let tech = ref("");

    const add = function () {

      /*j'envoie add au parent avec la valeur de tech*/
      ctx.emit("add", tech.value);
      tech.value = '';
    }

    return {
      tech,
      add,
    }
  }
}
</script>

<style scoped>

</style>