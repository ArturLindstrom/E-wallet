<template>
  <div class="add-card">
    <h1>ADD A NEW CARD</h1>
    <p class="new-card">NEW CARD</p>
      <NewCardForm @card="renderCard" :cards="cards" @send="sendCard"/>
  </div>
</template>

<script>
import NewCardForm from "../components/NewCardForm.vue"

export default {
  props:{cards:Array},
  
    data(){return{
    }},
  components: {NewCardForm},
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
  padding: 1rem;
}
.new-card{
  margin: 0;
}

h1{
  margin: 0;
}
</style>