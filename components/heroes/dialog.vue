<template>
  <v-dialog v-model="open_dialog" max-width="500px">
    <v-card>
      <v-card-title></v-card-title>
      <v-toolbar color="primary" text-align="center"><v-toolbar-title class="text-center">{{ character.name
      }}</v-toolbar-title>
      </v-toolbar>
      <v-card-text>
        <v-img :src="character.thumbnail.path + '.' + character.thumbnail.extension"></v-img>
        <h2>Description:</h2>
        <p>{{ character.description || "No information found" }}</p>
        <h2>Number of comics:</h2>
        <p>{{ character.comics.available + " comics" || "No information found" }}</p>
        <h2>Number of series:</h2>
        <p>{{ character.series.available + " series" || "No information found" }}
        </p>
        <h2>Number of stories:</h2>
        <p>{{ character.stories.available + " stories" || "No information found" }}</p>
        <h2>Number of events:</h2>
        <p>{{ character.events.available + " events" || "No information found" }}</p>
        <h2>Some series:</h2>
        <v-list lines="one">
          <v-list-item v-for="(series, index ) in character.series.items.slice(0, 3)"  :key="series.id" >
            <v-list-item-title>{{ series.name }}</v-list-item-title>
          </v-list-item>
        </v-list>
      </v-card-text>
      <v-card-actions>
        <v-btn color="primary" @click="closeDialog">Close</v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>


<script setup>
const open_dialog = ref(false)
/* const character_dialog=ref({}) */
const character = ref({})

const props = defineProps({
  dialog: {
    type: Boolean,
    required: true
  },
  character: {
    type: Object,
    required: true
  }
})
onBeforeMount(() => {
  open_dialog.value = props.dialog
  character.value = props.character
})

const emit = defineEmits(['close'])

const closeDialog = () => {
  // Método para cerrar el diálogo
  emit("close"); // Emite un evento para cerrar el diálogo
}


</script>

<style>
h2 {
  color: rgb(162, 10, 233)
}
v-list-item-title{
  font-family: Arial, sans-serif;
}
</style>





