<template>
  <h1>Characters</h1>
  <div>
    <v-card class="mx-auto" max-width="344" v-for="item in characters" :key="item.id">
      

      <v-img
        src="`(item.thumbnail.path.concat(item.thumbnail.extension)´)"
        height="200px"
      ></v-img>

      <v-card-title> Top western road trips </v-card-title>

      <v-card-subtitle> 1,000 miles of wonder </v-card-subtitle>

      <v-card-actions>
        <v-btn color="orange lighten-2" text> Explore </v-btn>

        <v-spacer></v-spacer>

        <v-btn icon @click="show = !show">
          <v-icon>{{ show ? "mdi-chevron-up" : "mdi-chevron-down" }}</v-icon>
        </v-btn>
      </v-card-actions>

      <v-expand-transition>
        <div v-show="show">
          <v-divider></v-divider>

          <v-card-text>
            I'm a thing. But, like most politicians, he promised more than he could
            deliver. You won't have time for sleeping, soldier, not with all the bed
            making you'll be doing. Then we'll go with that data file! Hey, you add a one
            and two zeros to that or we walk! You're going to do his laundry? I've got to
            find a way to escape.
          </v-card-text>
        </div>
      </v-expand-transition>
    </v-card>
  </div>
</template>
<script setup>
import axios from "axios";
const character = ref({});
const ruta=ref()
onBeforeMount(() => {
  datos();
});

const datos = async () => {
  const { data } = await axios.get(
    "https://gateway.marvel.com:443/v1/public/characters?ts=10&apikey=c920b676d987c6ae7beaa27cc956a376&hash=7b625305993dfaf0623804a3a799e432"
  );

  character.value=data.data.results
  console.log(data);
  console.log(character);
};
</script>
<script>
export default {
  data: () => ({
    show: false,
  }),
};
</script>
<style>
.div {
  display: grid;
  grid-template-columns: auto auto auto;
}
</style>
