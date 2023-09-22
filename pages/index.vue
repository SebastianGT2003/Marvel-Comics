<template>
  <div>
    <h1>Hola</h1>
  </div>
</template>
<script setup>

const router = useRouter()


const user = ref({});

definePageMeta({
  layout: "default",
});

const consola = () => {
  if (user.value.correo==="Sebas@gmail.com" && user.value.contraseña==="sebas123"){
    router.push({
      path: "/tareas"
    })
  }
  else{
    alert('Usuario incorrecto')
  }

};
</script>
