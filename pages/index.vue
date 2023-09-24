<template>
  <h1>Characters</h1>
  <div class="container">
    <div class="card-container" v-for="item in characters" :key="item.id">
      <v-card class="card-image mx:10">
        <v-img :src="item.thumbnail.path + '.' + item.thumbnail.extension" height="400px" cover></v-img>
        <v-card-title> {{ item.name }} </v-card-title>
        <v-card-actions>
          <v-btn color="orange-lighten-2" variant="text" @click="show_dialog(item.id)">
            Explore
          </v-btn>

          <v-spacer></v-spacer>

        </v-card-actions>

      </v-card>
    </div>

  </div>
  <heroes-dialog v-if="open_dialog" :character="character_dialog" :dialog="open_dialog" @close="close_dialog" />


</template>
<script setup>
import axios from "axios";


const router = useRouter()

const characters = ref({});

const open_dialog= ref(false)

const character_dialog=ref({})



onBeforeMount(() => {
  datos();
});



const datos = async () => {
  const { data } = await axios.get(
    "https://gateway.marvel.com:443/v1/public/characters?ts=10&apikey=c920b676d987c6ae7beaa27cc956a376&hash=7b625305993dfaf0623804a3a799e432&limit=100"
  );

  characters.value = data.data.results.filter(characters=>{
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
  // Cerramos el diálogo
  open_dialog.value = false;
};
</script>

<style>
.container {
  display: grid;
  grid-template-columns: 25% 25% 25% 25%;
  flex-wrap: wrap;
  justify-content: space-around;
  align-content: space-between;
  padding: 20px;
  box-sizing: border-box;
  
  
}

.card-container {
  flex-basis: calc(25% - 30px); /* Ajusta el tamaño base para mostrar 4 tarjetas por fila */
  margin: 10px;
  display: flex;
  justify-content: center;
  align-items: flex-end;
  box-sizing: border-box; /* Incluye el espacio del margen en el tamaño total */
}

.card-image  {
  width: 100%;
  /* max-width: 200px; */
  height: 100%;
}

@media (max-width: 767px) {
  .card-image {
  width: 100%;
  max-width: 150px;
  max-height: 800px;
  object-fit: cover;
}
.card-container {
  flex-basis: calc(25% - 30px); /* Ajusta el tamaño base para mostrar 4 tarjetas por fila */
  margin: 10px;
  display: flex;

}
.container {
  display:grid;
  grid-template-columns: 50% 50%;
  flex-wrap: wrap;
  justify-content: space-around;
  align-content: space-between;
  padding: 20px;
  box-sizing: border-box;
  
  
}


}
@media (min-width: 767px) and (max-width: 900px) {
  .container {
    display: grid;
    grid-template-columns: 33% 33% 33%;
    flex-wrap: wrap;
    justify-content: space-around;
    align-content: space-between;
    padding: 20px;
    box-sizing: border-box;
  }
}


</style>
