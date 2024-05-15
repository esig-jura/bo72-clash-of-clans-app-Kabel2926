<script setup>
import {useRoute} from "vue-router";

//récupérer un paramètre de l'URL de la route

const route = useRoute();



</script>

<template>
    <h1>Troupe n° {{route.params.id}}</h1>
</template>

<style>

</style>


