<template>
  <v-dialog v-model="open_dialog" max-width="500px">
    <v-card>
      <v-card-title>Explore Character</v-card-title>
      <v-card-text>
        <!-- Contenido del diálogo -->
        <!-- Puedes personalizar el contenido aquí -->
      </v-card-text>
      <v-card-actions>
        <v-btn color="primary" @click="closeDialog">Cerrar</v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>


<script setup>
const open_dialog = ref(false)
/* const character_dialog=ref({}) */
const character=ref({})

const props = defineProps({
    dialog: {
        type: Boolean,
        required: true
    },
    character:{
      type: Object,
      required:true
    }
})
onBeforeMount(() => {
  open_dialog.value = props.dialog
  character.value=props.character
})

const emit = defineEmits(['close'])

const closeDialog=()=> {
      // Método para cerrar el diálogo
      emit("close"); // Emite un evento para cerrar el diálogo
    }


</script>





