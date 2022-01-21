<template>
  <div class="add-card">
    <h1>ADD A NEW CARD</h1>
      <Card :card="card" />
      <NewCardForm @emit="renderCard" :cards="cards" @send="sendCard"/>
  </div>
</template>

<script>
import NewCardForm from "../components/NewCardForm.vue"
import Card from "../components/Card.vue"

export default {
  props:{cards:Array},
  
    data(){return{
      card: {}
    }},
  components: {NewCardForm, Card},
//   components: {NewCardForm},
  methods: {
    renderCard(event){
      this.card = event
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