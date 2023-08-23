<template>
  <section>
    <div class="d-flex flex-md-column flex-lg-row home-container">
      <div class="first-stage">
        <div class="col-lg-10 first-card py-3">
          <div class="d-flex">
            <div class="second-circle"></div>
            <div class="mt-2 ml-2 circle"></div>
            <div class="mt-3 text">Debit Dollar</div>
          </div>
          <div class="mt-4 d-flex align-item-center">
            <p class="text-1 ml-3">{{cardNum}}</p>
          </div>
          <div class="d-flex justify-content-between align-item-center">
            <p class="name ml-3">{{cardN}}</p>
            <div class="d-flex">
              <p class="num" v-if="selectedMonth">{{cardM}}</p>
              <p class="num">{{s}}</p>
              <p class="num mr-3">{{cardY}}</p>
            </div>
          </div>
        </div>
        <div class="py-2 second-card">
          <div class="mt-2 logo"></div>
          <div class="cvv-logo d-flex justify-content-end">
            <p class="digit mr-3">{{cardC}}</p>
          </div>
          <div class="mt-4 d-flex flex-column mb-5">
            <div class="d-flex justify-content-center ">
              <span class="design-1"></span>
              <span class="design-2 ml-2"></span>
              <span class="design-3 ml-2"></span>
              <span class="design-4 ml-2"></span>
            </div>
            <div class="d-flex justify-content-center mt-1">
              <span class="design-5"></span>
              <span class="design-6 ml-2"></span>
              <span class="design-7 ml-2"></span>
              <span class="design-8 ml-2"></span>
            </div>
            <div class="d-flex justify-content-center mt-1">
              <span class="design-9"></span>
              <span class="design-10 ml-2"></span>
              <span class="design-11 ml-2"></span>
              <span class="design-12 ml-2"></span>
            </div>
          </div>
          <div></div>
        </div>
      </div>
      <div class="second-stage d-flex justify-content-center align-items-center">
        <div class="col-lg-7 next">
          <p class="h4 text-right text-primary">VueJs</p>
          <form v-if="!submitted" action="" @submit.prevent="cardInput">
            <div class="form-group">
              <label for="name">Cardholder name</label><br>
              <input type="text" class="form-control" placeholder="e.g. Jane appleseed " v-model="CardName" @input="nameInput" @paste="nameInputPaste" maxlength="20"/>
              <p v-if="error.general" class="error">{{ error.general }}</p>
              <p v-if="error.CardName" class="error">{{ error.CardName }}</p>
              <p></p>
            </div>
            <div class="form-group">
              <label for="number">card number</label><br>
              <input type="text" ref="input1" class="form-control" placeholder="e.g. 1234 5678 9123 0000" v-model="CardNumber" maxlength="19" @input="numberInput"/>
              <p v-if="error.general" class="error">{{ error.general }}</p>
              <p v-if="error.CardNumber" class="error">{{ error.CardNumber }}</p>
              <p v-if="error.CardNum" class="error">{{ error.CardNum }}</p>
            </div>
            <div class="d-flex justify-content-between gap-label">
              <div class="form-group">
                <label for="ex.date">exp. date (mm/yy)</label><br>
                <div class="d-flex gap-x">
                  <div class="width mr-3-form">
                    <select class="form-control uptown" v-model="selectedMonth">
                      <option v-for="(month, index) in months" :key="index" :value="month">
                        {{ month }}
                      </option>
                    </select>
                    <p v-if="error.general" class="error">{{ error.general }}</p>
                    <p v-if="error.Month" class="error">{{ error.Month }}</p>
                  </div>
                  <div class="width">
                    <input type="text" ref="input2" class="form-control uptown" placeholder="e.g. YY" v-model="CardYear" @input="yearInput" maxlength="2"/>
                    <p v-if="error.general" class="error">{{ error.general }}</p>
                    <p v-if="error.CardYear" class="error">{{ error.CardYear }}</p>
                  </div>
                </div>
              </div>
              <div class="form-group">
                <label for="cvv">cvv</label><br>
                <input type="text" ref="input3" class="form-control" placeholder="e.g. 123" v-model="CardCvv" maxlength="3" @input="cvvInput"/>
                <p v-if="error.general" class="error">{{ error.general }}</p>
                <p v-if="error.CardCvv" class="error">{{ error.CardCvv }}</p>
              </div>
            </div>
            <div class="d-flex justify-content-center">
              <button class="btn-color">Confirm</button>
            </div>
          </form>
          <div v-else class="thank">
            <img src="../assets/image/icon-complete.svg" alt="completed">
            <h1>Thank you!</h1>
            <p>We've added your card details</p>
            <button @click="Restart">Continue</button>
          </div>
        </div>
      </div>
    </div>
    <div class="attribution">
      <p> &copy;.copyright 2023 coded by Aniebiet</p>
    </div>
  </section>
</template>

<script>
import CardInfo from '@/components/CardInfo.vue';
export default {
  components: { CardInfo },
  data(){
    return{
      selectedMonth: 'MM',
      submitted: false,
      months: [
        'MM', '01', '02', '03', '04', '05', '06', '07', '08', '09', '10', '11', '12'
      ],
      CardName: "",
      CardNumber: "",
      CardYear: "",
      CardCvv: "",
      CardNum: "",
      error: {},
      cardNum: '0000 0000 0000 0000',
      cardN: 'Jane appleseed',
      cardM: 'MM',
      cardY: 'YY',
      s: '/',
      cardC: '000',
    };
  },
  methods: {
    nameInput(e){
      // Checks if the value entered into the input field is a digit or mathematical operators and prevent it
      this.CardName = this.CardName.replace(/[0-9+\-*/]/g, '');

      if(!this.CardName){
        this.error = {};
        this.error.CardName = "*Name required";
      }else{
        this.error.CardName = "";
      }
    },

    nameInputPaste(e){
      // Checks and prevent copying of numbers into the input field
      const pastText = e.clipboardData.getData('text')
      const filterText = pastText.replace(/[0-9]/g, "");

      setTimeout(() => {
        this.CardName = filterText;
      }, 0);

      e.preventDefault();
    },

    numberInput(e){
      const inputVal = this.CardNumber

      this.error= {};

      // Remove spaces and update inputValue
      this.CardNumber = e.target.value.replace(/\s/g, '');

      // Checks if the input field is in a wrong format
      if (!this.CardNumber) {
        this.error = {};
        this.error.CardNumber = "*Card number required";
      }else if(!this.onlyNum(inputVal)){
        this.error = {}
        this.error.CardNum = "*Wrong format, Numbers only";
      }else{
        this.error.CardNum = "";
        this.error.CardNumber = "";
      }

      // Your logic for handling input in the first input field
      if (this.CardNumber.length === 16) {
        // Move to the next input automatically
        this.focusNextInput(2);
      }
    },

    yearInput(){
      // Prevents letters and mathematical operators from entering the field
      this.CardYear = this.CardYear.replace(/[a-zA-Z+\-*/]/g, '');

      // Your logic for handling input in the first input field
      if (this.CardYear.length === 2) {
        // Move to the next input automatically
        this.focusNextInput(3);
      }
    },
    
    cvvInput(){
      // Prevents letters and mathematical operators from entering the field
      this.CardCvv = this.CardCvv.replace(/[a-zA-Z+\-*/]/g, '');
    },

    onlyNum(input){
      // Checks if a digit is entered into the field and allows it. Else help the CardNumber field to throw back an error message
      let inputNum = /^[0-9]+$/;
      return inputNum.test(input)
    },

    focusNextInput(nextInputNumber) {
      // Focus on the next input field if it exists
      const nextInputRef = this.$refs[`input${nextInputNumber}`];
      if (nextInputRef) {
        nextInputRef.focus();
      }
    },

    cardInput(){
      if( !this.CardName && !this.CardNumber && !this.selectedMonth && !this.CardYear && !this.CardCvv){
        this.error = {};
        this.error.general = "*Input required"
      } else if (!this.CardName) {
        this.error = {};
        this.error.CardName = "*Name required";
      }else if (!this.CardNumber) {
        this.error = {};
        this.error.CardNumber = "*Card number required";
      }else if (this.selectedMonth === 'MM') {
        this.error = {};
        this.error.Month = "*Invalid month";
      }else if (!this.CardYear) {
        this.error = {};
        this.error.CardYear = "*Card year required";
      }else if (!this.CardCvv){
        this.error = {};
        this.error.CardCvv = "*Card cvv required";
      }else{
        this.cardNum = this.seperateInput
        this.cardN = this.CardName 
        this.cardM = this.selectedMonth
        this.cardY = this.CardYear
        this.cardC = this.CardCvv
        this.submitted = true
      }
    },

    // To restart the page
    Restart(){
      this.submitted = false
      window.location.reload()
    }
  },
  computed: {
    seperateInput(){
      let first = this.CardNumber.split('').slice(0, 4).join('')
      let second = this.CardNumber.split('').slice(4, 8).join('')
      let third = this.CardNumber.split('').slice(8, 12).join('')
      let fourth = this.CardNumber.split('').slice(12, 16).join('')
      let full = first.toString() + ' ' + second.toString() + ' ' + third.toString() + ' ' + fourth.toString()
      return full
    },
    CardNumber(){
       // Remove existing spaces and format input with spaces between digits
      const cleanedInput = this.CardNumber.replace(/\s/g, '');
      const formatted = cleanedInput.replace(/(\d{4})/g, '$1 ');

      return formatted.trim();
    }
  }
}
</script>

<style>
*{
  padding: 0;
  margin: 0px;
  box-sizing: border-box;
}  
:root{
  --White: hsl(0, 0%, 100%);
  --Lightgrayishviolet: hsl(270, 3%, 87%);
  --Darkgrayishviolet: hsl(279, 6%, 55%);
  --Verydarkviolet: hsl(278, 68%, 11%);
}
.home-container{
  width: 100%;
}
@media screen and (max-width: 425px) {
  .home-container{
    flex-direction: column !important;
  }
}
.first-stage{
  width: 30%;
  background: linear-gradient(130deg, hsl(278, 94%, 30%) 15%, hsl(249, 99%, 64%)35%, hsl(278, 68%, 11%)65%);
  height: 100vh;
}
@media screen and (max-width: 900px) {
  .first-stage{
    display: flex;
    flex-direction: column-reverse;
    width: 100%;
    height: 57vh;
  }
}
.second-stage{
  width: 70%;
}
@media screen and (max-width: 768px) {
  .second-stage{
    width: 80%;
  }
}
@media screen and (max-width: 425px) {
  .second-stage{
    width: 100%;
    padding: 0 16px;
  }
}
.next{
  padding: 20px 9px;
  margin-left: 3em;
  width: 100%;
  height: fit-content;
  background: rgba(0, 0, 0, 0.103)
}
@media screen and (max-width: 1024px) {
  .next{
    margin: 0 0 0 8em;
  }
}
@media screen and (max-width: 768px) {
  .next{
    margin: 5em 0 1.5em 0;
    left: 14%;
  }
}
@media screen and (max-width: 425px) {
  .next{
    left: 0;
  }
}
.first-card{
  left: 35%;
  top: 16%;
  border-radius: 7px;
  background: linear-gradient(120deg,  hsl(278, 94%, 30%)15%, hsl(278, 94%, 45%) 30%, hsl(320, 94%, 45%) 70%, hsl(249, 99%, 64%)90%) ;
}
@media screen and (max-width: 1024px) {
  .first-card{
    max-width: 98% !important;
  }
}
@media screen and (max-width: 900px) {
  .first-card{
    position: relative !important;
    width: 46% !important;
    left: 6%;
    z-index: 1;
  }
}
@media screen and (max-width: 425px) {
  .first-card{
    width: 79% !important;
    left: 4%;
  }
}
@media screen and (max-width: 375px) {
  .first-card{
    width: 87% !important;
  }
}
@media screen and (max-width: 320px) {
  .first-card{
    width: 95% !important;
    left: 1.3%;
  }
}
.second-circle{
  border-radius: 50%;
  background: #fff;
  height: 35px;
  width: 35px;
}
.circle{
  border-radius: 50%;
  height: 15px;
  width: 15px;
  border: 1px solid #fff;
}
.text{
  color: #fff;
  margin-left: 50%;
}
@media screen and (max-width: 1024px) {
  .text{
    margin-left: 42%;
  }
}
@media screen and (max-width: 768px) {
  .text{
    margin-left: 50%;
  }
}
@media screen and (max-width: 320px) {
  .text{
    margin-left: 42%;
  }
}
.text-1{
  color: #fff;
  font-size: 25px;
}
.name, 
.num, 
.digit{
  color: #fff;
  font-size: 15px;
  text-transform: uppercase;
}
.second-card{
  position: relative;
  left: 60%;
  top: 20%;
  width: 84%;
  border-radius: 7px;
  background: hsl(0, 11%, 87%) ;
}
@media screen and (max-width: 1024px) {
  .second-card{
    width: 98% !important;
    left: 54%;
  }
}
@media screen and (max-width: 900px) {
  .second-card{
    position: relative !important;
    width: 46% !important;
    left: 25%;
    top: 40%;
  }
}
@media screen and (max-width: 425px) {
  .second-card{
    width: 79% !important;
    left: 17%;
  }
}
@media screen and (max-width: 375px) {
  .second-card{
    width: 87% !important;
    left: 11%;
  }
}
@media screen and (max-width: 320px) {
  .second-card{
    width: 95% !important;
    left: 3%;
  }
}
.logo{
  height: 40px;
  width: 100%;
  background: hsl(0, 1%, 25%);
}
.cvv-logo{
  margin-top: 15px;
  margin-left: 30px;
  height: 20px;
  border-radius: 5px;
  width: 80%;
  background: hsl(0, 2%, 72%);
}
.design-1, 
.design-12{
  background: hsl(0, 2%, 72%);
  width: 30%;
  height: 4px;
}
.design-2, 
.design-3, 
.design-10, 
.design-11{
  background: hsl(0, 2%, 72%);
  width: 5%;
  height: 4px;
}
.design-4, 
.design-8, 
.design-9{
  background: hsl(0, 2%, 72%);
  width: 2%;
  height: 4px;
}
.design-5{
  background: hsl(0, 2%, 72%);
  width: 4%;
  height: 4px;
}
.design-6{
  background: hsl(0, 2%, 72%);
  width: 11%;
  height: 4px;
}
.design-7{
  background: hsl(0, 2%, 72%);
  width: 14%;
  height: 4px;
}
input{
  text-transform: capitalize;
}
input[type="number"]::-webkit-inner-spin-button,
input[type="number"]::-webkit-outer-spin-button{
  -webkit-appearance: none;
  margin: 0;
}
label{
  text-transform: uppercase;
  font-weight: 600;
}
.width{
  width: 120px;
}
@media screen and (max-width: 1024px) {
  .gap-label{
    gap: 10px;
  }
}
@media screen and (max-width: 425px) {
  .width{
    width: 84px;
  }
  .gap-label{
    gap: 10px;
  }
  .gap-x{
    gap: 10px;
  }
}
@media screen and (max-width: 320px) {
  .gap-label{
    gap: 3px;
  }
  .gap-x{
    gap: 3px;
  }
}
.mr-3-form{
  margin-right: 1rem;
}
@media screen and (max-width: 425px) {
  .mr-3-form{
    margin-right: 0px!important;
  }
}
.btn-color{
  font-size: 18px;
  background: hsl(255, 78%, 18%);
  border: none;
  border-radius: 5px;
  color: #fff;
  padding: 10px 0px;
  margin-top: 20px;
  width: 100%;
}
.error{
  font-size: 12px;
  text-transform: capitalize;
  color: hsl(0, 95%, 49%);
}
.attribution{
  text-align: right;
  font-size: 20px;
  font-weight: 600;
  margin-top: -65px;
  padding: 0 30px 0 0;
}
@media screen and (max-width: 1024px) {
  .attribution{
    margin: -50px 0 0 -78px;
  }
}
@media screen and (max-width: 768px) {
  .attribution{
    margin: 0;
    padding: 0;
    text-align: center;
  }
}
@media screen and (max-width: 320px) {
  .attribution{
    font-size: 17px;
  }
}
.thank{
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 1em;
}

.thank h1{
  text-transform: uppercase;
  letter-spacing: 3px;
}
@media screen and (max-width: 320px) {
  .thank h1{
    letter-spacing: 2px;
  }
}
.thank p{
  font-size: 18px;
  color: var(--Darkgrayishviolet);
}

.thank button{
  color: var(--White);
  width: 100%;
  border-radius: 6px;
  padding: 10px 0px;
  border: none;
  font-size: 18px;
  background-color: var(--Verydarkviolet);
  cursor: pointer;
}
</style>
