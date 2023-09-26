<template>
  <div class="inicio">
    <h1 class="title">SUPERHEROS</h1>
    <div class="container">
      <div class="card-container" v-for="item in characters" :key="item.id">
        <v-card class="card-image mx:10">
          <v-img :src="item.thumbnail.path + '.' + item.thumbnail.extension" height="400px" cover></v-img>
          <v-card-title> {{ item.name }} </v-card-title>
          <v-card-actions>
            <v-btn :style="{ backgroundColor: 'rgb(162, 10, 233)', color: 'white' }" variant="text"
              @click="show_dialog(item.id)">
              Explore
            </v-btn>

            <v-spacer></v-spacer>

          </v-card-actions>

        </v-card>
      </div>

    </div>
    <heroes-dialog v-if="open_dialog" :character="character_dialog" :dialog="open_dialog" @close="close_dialog" />
  </div>
</template>
<script setup>
import axios from "axios";


const router = useRouter()

const characters = ref({});

const open_dialog = ref(false)

const character_dialog = ref({})



onBeforeMount(() => {
  datos();
});



const datos = async () => {
  const { data } = await axios.get(
    "https://gateway.marvel.com:443/v1/public/characters?ts=10&apikey=c920b676d987c6ae7beaa27cc956a376&hash=7b625305993dfaf0623804a3a799e432&limit=100"
  );

  characters.value = data.data.results.filter(characters => {
    return characters.thumbnail.path !== "http://i.annihil.us/u/prod/marvel/i/mg/b/40/image_not_available";

  })

  console.log(data);
  console.log(characters);
};

const show_dialog = (id_character) => {
  character_dialog.value = characters.value.find(character => character.id === id_character);
  open_dialog.value = true;
};

const close_dialog = () => {
  open_dialog.value = false;
};
</script>

<style >
@import "../styles/index.module.css";

</style>
