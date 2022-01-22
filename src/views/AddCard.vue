<template>
  <div class="add-card">
    <h1>ADD A NEW CARD</h1>
      <Card :card="card" />
      <NewCardForm @card="renderCard" :cards="cards" @send="sendCard"/>
  </div>
</template>

<script>
import NewCardForm from "../components/NewCardForm.vue"
import Card from "../components/Card.vue"

export default {
  props:{cards:Array},
  
    data(){return{
      card: {
        cardNumber: "XXXX XXXX XXXX XXXX", 
          cardHolder: "FIRSTNAME LASTNAME", 
          expireMonth: "MM", 
          expireYear: "YY", 
      }
    }},
  components: {NewCardForm, Card},
  methods: {
    renderCard(payload){
      this.card = payload
    },
    sendCard(newCard){
      this.$emit('sendMore', newCard)
  
    }
  }
}
</script>

<style>
.add-card{
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>