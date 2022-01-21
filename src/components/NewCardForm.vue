<template>
  <form @submit.prevent="pushNewCard" @input="cardPreview">
    <div class="num">
      <p>CARD NUMBER</p>
      <input type="text" maxlength="16" v-model="newCard.cardNumber" onkeypress="return /[0-9]/i.test(event.key)">
    </div>
    <div class="name-section">
      <p>CARDHOLDER NAME</p>
      <input type="text" maxlength="20" v-model="newCard.cardHolder" onkeypress="return /[a-ö, ' ']/i.test(event.key)" >
    </div>
      <p>VALID THRU</p>
      <div class="expiry">
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
      <input type="text" maxlength="3" onkeypress="return /[0-9]/i.test(event.key)" v-model="newCard.CCV">
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
          errorMessage: ""
        }
},
    methods:{
        cardPreview(){
            this.$emit('emit', this.newCard)
        },
        pushNewCard(){
          if(this.cards.find((vendor) => vendor.vendor == this.newCard.vendor)){
            this.errorMessage = `Du har redan ett kort från den banken!`
          } else if (this.cards.find((number) => number.cardNumber == this.newCard.cardNumber)){
            this.errorMessage ='Det finns redan ett kort med det numret!'
          } else {
            this.errorMessage = ""
            this.$emit('send',{...this.newCard})
          }
        }
    }
}
</script>

<style scoped>

p {
  margin-bottom: 0.2rem;
}

input {
  height: 2rem;
  font-size: 1.5rem;
}

.expiry {
  display: flex;
  width: 50%;
}

select {
  height: 2rem;
}

select, option {
  font-size: 1rem;
}


</style>