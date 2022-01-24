<template>
  <div class="home">
    <h1>E-WALLET</h1>
    <div class="active-card" v-if="activeCard">
      <span>active card</span>
      <Card :card="activeCard"/>
    </div>
    <div class="card-stack">
      <Card v-for="card in filterActive" :key="card.cardNumber" @click="()=>makeActive(card)" :card="card"/>
    </div>
    <button @click="$emit('changeView')">ADD A NEW CARD</button>
  </div>
</template>

<script>
import Card from "../components/Card.vue"

export default {
  props:{cards: Array},
  components: {Card},
  methods:{
    makeActive(card){
      this.activeCard = card
    }
  },
  computed:{
    filterActive(){
      return this.cards.filter(card => card != this.activeCard)
    }
  },
    data(){return{
      activeCard: this.cards[0]
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
  margin-bottom:.2rem ;
  text-transform: uppercase;
  font-family: 'Source Sans Pro', sans-serif;
  color: darkgray;
}

.active-card {
  margin-bottom: 2rem;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

button {
  border-radius: 8px;
  width: 23rem;
  padding: 1rem;
  background: white;
  border: solid black 2px;
  font-size: 1.4rem;
  font-weight: 700;
  margin-top: 5rem;
}

button :active{
  background: black;
  color: white;
  
}

.card-stack div {
  position: relative;
}

.card-stack {
  max-height: 20rem;
}

.card-stack div:first-child {
  margin-top: 0rem;
  transform: translateY(0rem)
}

.card-stack div:nth-of-type(2) {
  top: -10rem;
}

.card-stack div:nth-of-type(3){
  top: -20rem;
}




</style>