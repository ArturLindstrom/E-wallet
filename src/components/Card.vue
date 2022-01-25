<template>
  <div class="card" :class="classGenerator" @click="$emit('click')">
    <div class="wifichip">
      <img class="wifi" v-if="classGenerator == '' || classGenerator == 'bitcoin'" src="../assets/wifi.svg">
      <img class="wifi-white" v-else src="../assets/wifi_white.svg">
      <div class="chipcontainer">
        <img class="chip" src="../assets/chip.svg">
      </div>
    </div>
    <img v-if="this.newCard.vendor" v-bind:src="this.imgSrc" class="vendor-img">
    <p class="card-number">{{number}}</p>
    <div class="card-holder">
      <p card-holder-title>CARDHOLDER NAME</p>
      <p class="card-holder-name">{{name}}</p>
    </div>
    <div class="valid-date">
      <p>VALID THRU</p>
      <p class="exp-date">{{newCard.expireMonth}}/{{newCard.expireYear}}</p>
    </div>
  </div>
</template>

<script>
export default {
  props: {card: Object},
  computed: {
    newCard(){
      return this.card
    },
    
    imgSrc() {
      return require("../assets/" + (this.newCard.vendor) + ".svg")
    },
    classGenerator(){
      return this.newCard.vendor
    },
      name(){
            if(this.newCard.cardHolder == ""){
               return "FIRSTNAME LASTNAME"
            } else{

              return this.newCard.cardHolder.toUpperCase()
            }
        },
        number(){
            if(this.newCard.cardNumber == ""){
               return "XXXX XXXX XXXX XXXX"
            } else{

             return this.newCard.cardNumber.replace(/\d{4}(?=.)/g, '$& ')
            }
        }
  }
}
</script>

<style scoped>
p{
  color: black;
  text-shadow: 1px 0px 0px rgba(0, 0, 0, 0.15), 0px 1px 0px rgba(0, 0, 0, 0.05), -1px 0px 0px rgba(0, 0, 0, 0.05), 0px -1px 0px rgba(0, 0, 0, 0.15);

}

.card {
  display: grid;
  max-width: 21rem;
  width: 90vw;
  max-height: 13rem;
  height: calc(90vw*.618);
  aspect-ratio: 3.5/2;
  border-radius: 8px;
  background-color: darkgray;
  grid-template-areas: 
  "wifichip . . vendor-img"
  "card-number card-number card-number card-number "
  "card-holder . . valid-date";
  padding: 1rem;
  box-shadow: rgba(0, 0, 0, 0.35) 0px 5px 15px;
}


.vendor-img{
  grid-area: vendor-img;
  align-self: center;
  justify-self: center;
  height: 5rem;
}

.card-number{
  grid-area: card-number;
  font-size: 1.8rem;
  text-align: center;
  margin: 0;
  align-self: center;
}

.card-holder{
  grid-area: card-holder;
  align-self: flex-end;
}

.card-holder-title{
  margin: 0;
}

.card-holder-name, .exp-date{
  font-size: 1.2rem;
  margin: 0 0 2rem 0;
  line-height: 0;
}

.valid-date{
  grid-area: valid-date;
  text-align: right;
  align-self: flex-end;
}

.wifichip {
  display: flex;
  flex-direction: column;
  align-items: center;
  grid-area: wifichip;
  align-self: flex-start;
  justify-self: flex-start;
}

.wifi, .chip, .wifi-white {
  height: 2rem;
}

.chip {
  width: 3rem;
}

.wifi {
  opacity: 0.5;
}

.chipcontainer {
  background: #ECE6DF;
  border-radius: 8px;
}

.bitcoin{
  background: linear-gradient(248.04deg, rgba(255, 255, 255, 0.15) 0%, rgba(255, 255, 255, 0) 99.07%), #FFAE34;
}


.blockchain {
  background: linear-gradient(248.52deg, rgba(0, 0, 0, 0.15) 1.49%, rgba(0, 0, 0, 0) 100%), #8B58F9;
}
.blockchain p{
  color: white;
  
}

.evil {
  background: linear-gradient(248.3deg, rgba(0, 0, 0, 0.16) 0%, rgba(0, 0, 0, 0) 100%), #F33355;
}
.evil p{
  color: white;
  
}
.ninja {
 background: linear-gradient(248.3deg, rgba(255, 255, 255, 0.15) 0%, rgba(255, 255, 255, 0) 100%), #222222;
}

.ninja p{
  color: white;

}


</style>