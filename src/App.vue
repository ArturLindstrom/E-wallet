<template>
  <div id="app">
    <HomeView v-if="view=='HomeView'" :cards="cards" @changeView="view='AddCard'" @remove="removeCard" />
    <AddCard v-if="view=='AddCard'" :cards="cards" @sendMore="pushNewCard" @back="view='HomeView'"/>
    <DarkMode/>
  </div>
</template>

<script>
import HomeView from "./views/HomeView.vue";
import AddCard from "./views/AddCard.vue";
import DarkMode from "./components/DarkMode.vue"

export default {
  components: {HomeView, AddCard, DarkMode},
  beforeMount(){
    if(localStorage.cards){
      this.cards = JSON.parse(localStorage.getItem("cards"))
    }
  },
  methods: {
    pushNewCard(newCard){
      this.cards.push(newCard)
      this.view = "HomeView"
      localStorage.setItem('cards', JSON.stringify(this.cards))
    },
    removeCard(removeCard){
      for(let i = 0; i < this.cards.length; i++){
        if(removeCard == this.cards[i]) {
          this.cards.splice(i, 1)
        }
        localStorage.setItem('cards', JSON.stringify(this.cards))
      }
    }
    },

  data(){return{
    view: "HomeView",
    
    cards: [
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
  /* background: rgb(12, 10, 10); */
}
#app{
  display: flex;
  flex-direction: column;
  align-items: center;

}

h1 {
  font-family: 'Source Sans Pro', sans-serif;
}

p, span {
  font-family: 'PT Mono', monospace;
}

</style>