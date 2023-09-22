<template>
  <div class="layout">
    <v-img
      max-height="150"
      max-width="250"
      padding="10%"
      src="https://upload.wikimedia.org/wikipedia/commons/7/71/Marvel-Comics-Logo.svg"
    ></v-img>
  </div>
  <slot />
</template>
<script setup>

</script>
<style>
.layout {
  background-color: black;
  display: grid;
  grid-template-columns: auto auto auto;
/*   display: block; */
  height: 10%;
  width: auto;
}
</style>
