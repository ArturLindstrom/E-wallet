<template>
  <div class="add-card">
    <span class="back-button" @click="$emit('back')">&larr;</span>
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

.back-button{
  align-self: flex-start;
  justify-self: center;
  cursor: pointer;
  font-weight: 900;
  font-size: 2.5rem;
  position: absolute;
  
}

h1{
  margin: 0;
}
</style>