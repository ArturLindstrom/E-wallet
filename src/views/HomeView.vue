<template>
  <div class="home">
    <h1>E-WALLET</h1>
    <div class="active-card" v-if="activeCard">
      <span>active card</span>
      <Card :card="activeCard"/>
      <span class="remove-active" @click="showModal=true">REMOVE CARD</span>
      <div v-if="showModal" @click.self="showModal=false" class="modal-mask">
        <div class="modal">
        <span>Remove active card?</span>
        <div class="button-container">
          <button @click="removeActive">YES</button>
          <button @click="showModal=false">NO</button>
        </div>
        </div>
      </div>
    </div>
      <span>YOUR CARDS</span>
    <div class="card-stack" v-if="filterActive.length > 0">
      <Card v-for="card in filterActive" :key="card.cardNumber" @click="()=>makeActive(card)" :card="card"/>
    </div>
    <button class="add-card" @click="$emit('changeView')">ADD A NEW CARD</button>
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
    },
    removeActive(){
      this.$emit('remove', this.activeCard)
      this.activeCard = this.cards[0]
      this.showModal = false
    }
  
  },
  computed:{
    filterActive(){
      return this.cards.filter(card => card != this.activeCard)
    }
  },
    data(){return{
      activeCard: this.cards[0],
      showModal: false
    }}

}
</script>

<style scoped>
.home {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding-bottom: 1rem;
}
span {
  text-align: center;
  margin-bottom:.2rem ;
  text-transform: uppercase;
  font-family: 'Source Sans Pro', sans-serif;
  color: darkgray;
}

h1{
  margin: 0;
}

.active-card {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.remove-active{
  color: red;
  font-weight: 600;
  cursor: pointer;
}

.modal-mask{
  position: fixed; 
  z-index: 1; 
  left: 0;
  top: 0;
  width: 100%; 
  height: 100%; 
  overflow: auto; 
  background-color: rgb(0,0,0); 
  background-color: rgba(0,0,0,0.4); 
}

.modal {
  background-color: #fefefe;
  margin: 15% auto; 
  padding: 4rem;
  border: 2px solid black;
  width: 15rem;
  display: flex;
  justify-content: center;
  border-radius: 8px;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.modal span{
  font-size: 1.5rem;
  color: red;
  font-weight: 600;
}

.button-container{
  display: flex;
}

.modal button{
  width: 4rem;
  text-align: center;
  margin: 1rem;
  background: white;
  border: solid black 2px;
   font-size: 1.4rem;
  font-weight: 700;
  border-radius: 8px;
}

.add-card {
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

.card-stack {
  
  display: grid;
  grid-auto-rows: 4rem;
  margin-bottom: 9rem;
}

</style>