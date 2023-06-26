<template>
  <body>


    <div class="card-container">
      <p class="title-card text">Cena {{ numCena + 1 }} con el rey godo <span class="verde"> {{ rey }}</span></p>

      <div>
        <p class="text">Precio: <span class="verde">{{ productos[numCena].precio }}€</span></p>
        <p v-if="productos[numCena].precio < 100" class="text"> Ahorra un 10% dto: <span class="verde">{{ newPrice }}
            €</span> <img class="img" src="./assets/datos/oferta.jpg" alt=""></p>
        <p v-if="productos[numCena].finDeSemana == true" class="text finSemana-true">Solo fines de semana</p>
        <p v-else class="text finSemana-false">Todos los dias!</p>
      </div>
      <img :src="reyImg" alt="">
      <button @:click="siguiente" class="text">Siguiente ({{ numCena + 1 }} / {{ total }})</button>

    </div>
  </body>
</template>


<script setup>
import { ref } from 'vue';
import { computed } from 'vue'
import { productos } from "./assets/datos/datos"
const numCena = ref(0)
const total = productos.length
const priceKing = ref(110)
const ruta = ""

const siguiente = () => {

  numCena.value++

  if (numCena.value == total) {
    numCena.value = 0
  }

}

const rey = computed(() => {
  const nameLowCase = productos[numCena.value].nombre.toLowerCase()

  return nameLowCase.substring(0, 1).toUpperCase() + nameLowCase.substring(1)
})

const reyImg = computed(() => {
  const nameLowCase = productos[numCena.value].nombre.toLowerCase()
  return `https://www.html6.es/img/rey_${nameLowCase}.png`

})

const newPrice = computed(() => {
  return Number(productos[numCena.value].precio / 1.10).toFixed(2)
})

</script>

<style scoped>

body{
  display: flex;
  justify-content: center;
  align-items: center;
}
.card-container {
  width: 500px;
  height: 800px;
  border: 1px solid black;
  border-radius: 25px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.text {
  text-align: center;
  font-size: 2rem;
}

.title-card {
  font-size: 1.5rem;
}

.verde {
  color: green;
}

.finSemana-true {
  background-color: red;
  color: white;
  border-radius: 5px;
}

.finSemana-false {
  background-color: green;
  color: white;
  border-radius: 5px;
}

.img {
  width: 60px;
  height: 40px;
}
</style>


