<script setup>
// Cheat Sheet: https://steve-fallet.notion.site/Vue-3-script-setup-Cheat-Sheet-b12192ceae244ecda65f771579ca02bc
import {onMounted, ref} from "vue";
import PageTopBarre from "@/components/PageTopBarre.vue";
import PageHeader from "@/components/PageHeader.vue";
import PageFooter from "@/components/PageFooter.vue";
import TroupeCarte from "@/components/TroupeCarte.vue";

// Quand le composant est monté, on va chercher les données
onMounted(() => {
  fetch('https://cocapi.divtec.me/troupes')
      .then((res) => res.json())
      .then((data) => {
        troupes.value = data
      })
})


// Tableau des troupes
const troupes = ref([])

let TotalOr = ref(100000);

onMounted(() =>{
  fetch('https://cocapi.divtec.me/troupes')
      .then((res) => res.json())
      .then((data) => {
        troupes.value = data
      })
})

/* Méthodes */
function formerTroupe(troupe) {
  if (TotalOr.value < troupe.cout) {
    alert("Vous n'avez pas assez d'or mon seigneur !")
    return
  }
  TotalOr.value -= troupe.cout
  formerTroupe.value.push(troupe)
}

</script>
<template>
  <page-top-barre :or="TotalOr"/>
  <page-header/>
  <main>
    <ul class="cartes">
      <li  v-for="troupe in troupes" :key="troupe.id">
        <troupe-carte
            :troupe="troupe"
            :or="TotalOr"
            @former="formerTroupe"
        />
      </li>
    </ul>
  </main>
  <page-footer/>
</template>


