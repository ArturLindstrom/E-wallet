<template>
  <div id="app">
    <HomeView v-if="view=='HomeView'" :cards="cards" @changeView="view='AddCard'" />
    <AddCard v-if="view=='AddCard'" :cards="cards" @sendMore="pushNewCard"/>
  </div>
</template>

<script>
import HomeView from "./views/HomeView.vue";
import AddCard from "./views/AddCard.vue";

export default {
  components: {HomeView, AddCard},
  methods: {
    pushNewCard(newCard){
      this.cards.push(newCard)
      this.view = "HomeView"
    }
    },

  data(){return{
    view: "HomeView",
    
    cards: [
      {
      vendor: "bitcoin", 
      cardNumber: "1234 5678 9012 3456", 
      cardHolder: "Kent Aurén", 
      expireMonth: "3", 
      expireYear: "23", 
      CCV: '666'
      },
      // {
      // vendor: "Bitcoin", 
      // cardNumber: "1234 5678 9012 3156", 
      // cardHolder: "Kent Aurén", 
      // expireMonth: "3", 
      // expireYear: "23", 
      // CCV: '666'
      // }
    ]
  }}
}
</script>


<style>
@import url('https://fonts.googleapis.com/css2?family=PT+Mono&family=Source+Sans+Pro:wght@400;700&display=swap');

#app{
  padding: .5rem;
}

h1 {
  font-family: 'Source Sans Pro', sans-serif;
}

p, span {
  font-family: 'PT Mono', monospace;

}

</style>