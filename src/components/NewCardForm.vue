<template>
  <div class="form">
    <form @submit.prevent="pushNewCard" @input="cardPreview" autocomplete="off">
      <div class="num">
        <p>CARD NUMBER</p>
        <input type="text" maxlength="19" @keyup="numberSpacer" v-model="newCard.cardNumber" placeholder="XXXX XXXX XXXX XXXX" onkeypress="return /[0-9]/i.test(event.key)">
      </div>
      <div class="name-section">
        <p>CARDHOLDER NAME</p>
        <input type="text" maxlength="20" v-model="newCard.cardHolder" onkeypress="return /[a-ö, ' ']/i.test(event.key)" placeholder="FIRSTNAME LASTNAME">
      </div>
        <div class="expiry">
        <div class="flex">
          <p>VALID THRU</p>
          <select v-model="newCard.expireMonth">
              <option value="" disabled>MM</option>
              <option :value="month" v-for="month in 12" :key="month">
                  {{month}}
              </option>
          </select>
          <select v-model="newCard.expireYear">
              <option value="" disabled>YY</option>
              <option :value="year+2021" v-for="year in 10" :key="year">
                  {{year+2021}}
              </option>
          </select>
        </div>
      <div class="ccv">
        <p>CCV</p>
        <input type="text" class="ccv" maxlength="3" onkeypress="return /[0-9]/i.test(event.key)" v-model="newCard.CCV">
      </div>
      </div>
      <div class="vendor">
        <p>VENDOR</p>
        <select v-model="newCard.vendor" placeholder="sadadssd">
            <option value="bitcoin">BITCOIN INC</option>
            <option value="blockchain">BLOCK CHAIN INC</option>
            <option value="evil">EVIL CORP</option>
            <option value="ninja">NINJA BANK</option>
        </select>
      </div>
      <div class="submit">
        <p class="error">{{errorMessage}}</p>
        <button>ADD CARD</button>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  props: {cards: Array},
    data(){return{
      newCard:
          {
          vendor: "", 
          cardNumber: "", 
          cardHolder: "", 
          expireMonth: "", 
          expireYear: "", 
          CCV: ''
          },
          errorMessage: "",
        }},
    methods:{
        cardPreview(){
            this.$emit('card', this.newCard)
        },
        pushNewCard(){
          if(this.cards.find((vendor) => vendor.vendor == this.newCard.vendor)){
            this.errorMessage = `Du har redan ett kort från den banken!`
          } else if (this.cards.find((number) => number.cardNumber == this.newCard.cardNumber)){
            this.errorMessage ='Det finns redan ett kort med det numret!'
          } else if (this.newCard.vendor == ''){
            this.errorMessage = 'Du måste välja en bank!'
          } else {
            this.errorMessage = ""
            this.$emit('send',{...this.newCard})
          }
        },
       numberSpacer() {

           if (this.newCard.cardNumber.length == 4 || this.newCard.cardNumber.length == 9 || this.newCard.cardNumber.length == 14)
          this.newCard.cardNumber +=' ';
       }
    }
}
</script>

<style scoped>



form{
  display: flex;
  flex-direction: column;
  align-items: center;
}

p {
  margin-bottom: 0.2rem;
  /* text-align: ; */
}

.num, .name-section, .expiry, .vendor{
  width: 100%;
}

input {
  height: 2rem;
  width: 95%;
  padding: .5rem;
  font-size: 1rem;
  border-radius: 8px;
  font-family: 'PT Mono', monospace;
  color: black;
  text-transform: uppercase;
}

input::placeholder {
  color: black;
}

.expiry{
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.expiry select{
  margin: 0 1rem 0 0;
  /* width: 100%; */
  height: 3rem;
}

select {
  height: 2rem;
  border-radius: 8px;
  size: 2;
  border: solid black 2px;
}

.ccv{
  width: 12.5rem;
  margin-right: 1.1rem;
}

.vendor select{
  width: 100%
}

select, option {
  font-size: 1rem;
  
}

button{
   border-radius: 8px;
  width: 23rem;
  padding: 1rem;
  color: white;
  background: black;
  border: solid black 1px;
  font-size: 1.4rem;
  font-weight: 700;
}

.error{
  color: red;
}



</style>