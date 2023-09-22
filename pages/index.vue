<template>
  <h1>Characters</h1>
  <div class="container">
    <div class="card-container" v-for="item in characters" :key="item.id">
      <v-card class="card-image mx:10">
        <v-img :src="item.thumbnail.path + '.' + item.thumbnail.extension" height="200px" cover></v-img>
        <v-card-title> {{ item.name }} </v-card-title>
        <v-card-actions>
          <v-btn color="orange-lighten-2" variant="text">
            Explore
          </v-btn>

          <v-spacer></v-spacer>

          <v-btn :icon="show ? 'mdi-chevron-up' : 'mdi-chevron-down'" @click="show = !show"></v-btn>
        </v-card-actions>

        <v-expand-transition>
          <div v-show="show">
            <v-divider></v-divider>

            <v-card-text>
              I'm a thing. But, like most politicians, he promised more than he could deliver. You won't have time for
              sleeping, soldier, not with all the bed making you'll be doing. Then we'll go with that data file! Hey, you
              add a one and two zeros to that or we walk! You're going to do his laundry? I've got to find a way to
              escape.
            </v-card-text>
          </div>
        </v-expand-transition>
      </v-card>
    </div>

  </div>
</template>
<script setup>
import axios from "axios";
const characters = ref({});
onBeforeMount(() => {
  datos();
});

const datos = async () => {
  const { data } = await axios.get(
    "https://gateway.marvel.com:443/v1/public/characters?ts=10&apikey=c920b676d987c6ae7beaa27cc956a376&hash=7b625305993dfaf0623804a3a799e432"
  );

  characters.value = data.data.results
  console.log(data);
  console.log(characters);
};
</script>
<script>
export default {
  data: () => ({
    show: false,
  }),
}
</script>
<style>
.container {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
  align-content: space-between;
  height: 100vh;
  padding: 20px;
  box-sizing: border-box;
}

.card-container {
  flex-basis: calc(25% - 20px); /* Ajusta el tamaño base para mostrar 4 tarjetas por fila */
  margin: 10px;
  display: flex;
  justify-content: center;
  align-items: flex-end;
  box-sizing: border-box; /* Incluye el espacio del margen en el tamaño total */
}

.card-image {
  width: 100%;
  max-height: 800px;
  object-fit: cover;
}
</style>
