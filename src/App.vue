<template>
  <div id="app">
    <HomeView v-if="view=='HomeView'" :cards="cards" @changeView="view='AddCard'"  />
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
      // {
      // vendor: "bitcoin", 
      // cardNumber: "1234 5678 9012 3456", 
      // cardHolder: "Kent Aurén", 
      // expireMonth: "3", 
      // expireYear: "23", 
      // CCV: '666'
      // }
      // {
      // vendor: "blockchain", 
      // cardNumber: "1234 5678 9012 3156", 
      // cardHolder: "Kent Aurén", 
      // expireMonth: "3", 
      // expireYear: "23", 
      // CCV: '666'
      // },
      // {
      // vendor: "evil", 
      // cardNumber: "1337 1337 1337 1337", 
      // cardHolder: "OSCAR ARRHENIUS", 
      // expireMonth: "13", 
      // expireYear: "37", 
      // CCV: '666'
      // },
      // {
      // vendor: "ninja", 
      // cardNumber: "1338 1337 1337 1337", 
      // cardHolder: "OSCAR ARRHENIUS", 
      // expireMonth: "13", 
      // expireYear: "37", 
      // CCV: '666'
      // }
    ]
  }}
}
</script>


<style>
@import url('https://fonts.googleapis.com/css2?family=PT+Mono&family=Source+Sans+Pro:wght@400;700&display=swap');


body{
  margin: 0 auto;
  padding: 0;
  overflow-x: hidden;
}
#app{
  display: flex;
  flex-direction: column;
  align-items: center;

}

h1 {
  font-family: 'Source Sans Pro', sans-serif;
}

p {
  font-family: 'PT Mono', monospace;
}

</style>