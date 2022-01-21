<template>
  <div class="home">
    <h1>E-WALLET</h1>
    <span>Active card</span>
    <Card v-for="card in cards" :key="card.cardNumber" :card="card"/>
    <button @click="$emit('changeView')">ADD CARD</button>
  </div>
</template>

<script>
import Card from "../components/Card.vue"

export default {
  props:{
    cards: Array,
  },

  components: {Card},
    data(){return{

    }}

}
</script>

<style scoped>
.home {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
span {
  text-align: center;
}


</style>