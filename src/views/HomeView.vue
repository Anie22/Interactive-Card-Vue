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
              <p class="num">{{cardM}}</p>
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
          <form action="" @submit.prevent="cardInput">
          <div class="form-group">
            <label for="name">Cardholder name</label><br>
            <input type="card-name" class="form-control" placeholder="e.g. Jane appleseed " v-model="CardName"/>
            <p v-if="error.general" class="error">{{ error.general }}</p>
            <p v-if="error.CardName" class="error">{{ error.CardName }}</p>
            <p></p>
          </div>
          <div class="form-group">
            <label for="number">card number</label><br>
            <input type="card-name" class="form-control" placeholder="e.g. 1234 5678 9123 0000" v-model="CardNumber" maxlength="16"/>
            <p v-if="error.general" class="error">{{ error.general }}</p>
            <p v-if="error.CardNumber" class="error">{{ error.CardNumber }}</p>
          </div>
          <div class="d-flex justify-content-between gap-label">
            <div class="form-group">
              <label for="ex.date">exp. date (mm/yy)</label><br>
              <div class="d-flex gap-x">
                <div class="width mr-3-form">
                  <!-- <select 
                    class="form-control uptown" 
                    v-model="select" 
                    aria-label="Default select example"
                  >
                    <option :value="null">00</option>
                    <option v-for="(Month, index) in Month" :key="index">{{Month}}</option>
                  </select> -->
                  <input type="card-name" class="form-control uptown" placeholder="e.g. MM" v-model="Month" maxlength="2">
                  <p v-if="error.general" class="error">{{ error.general }}</p>
                  <p v-if="error.Month" class="error">{{ error.Month }}</p>
                </div>
                <div class="width">
                  <input type="card-name" class="form-control uptown" placeholder="e.g. YY" v-model="CardYear" maxlength="2">
                  <p v-if="error.general" class="error">{{ error.general }}</p>
                  <p v-if="error.CardYear" class="error">{{ error.CardYear }}</p>
                </div>
              </div>
            </div>
            <div class="form-group">
              <label for="cvv">cvv</label><br>
              <input type="card-name" class="form-control" placeholder="e.g. 123" v-model="CardCvv" maxlength="3"/>
              <p v-if="error.general" class="error">{{ error.general }}</p>
              <p v-if="error.CardCvv" class="error">{{ error.CardCvv }}</p>
            </div>
          </div>
          <div class="d-flex justify-content-center">
              <button class="btn-color">Confirm</button>
            </div>
          </form>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import CardInfo from '@/components/CardInfo.vue';
export default {
  components: { CardInfo },
  data(){
    return{
      select: null,
      CardName: "",
      CardNumber: "",
      Month: "",
      CardYear: "",
      CardCvv: "",
      error: {},
      cardNum: '0000 0000 0000 0000',
      cardN: 'Jane appleseed',
      cardM: 'MM',
      cardY: 'YY',
      s: '/',
      cardC: '000'
    };
  },
  methods: {
    cardInput(){

      if(
        !this.CardName &&
        !this.CardNumber &&
        !this.Month &&
        !this.CardYear &&
        !this.CardCvv
      ){
        this.error = {};
        this.error.general = "*Input required"
      } else if (!this.CardName) {
        this.error = {};
        this.error.CardName = "*Name required";
      }else if (!this.CardNumber) {
        this.error = {};
        this.error.CardNumber = "*Card number required";
      }else if (!this.Month) {
        this.error = {};
        this.error.Month = "*Card month required";
      }else if (!this.CardYear) {
        this.error = {};
        this.error.CardYear = "*Card year required";
      }else if (!this.CardCvv){
        this.error = {};
        this.error.CardCvv = "*Card cvv required";
      }else if(this.Month.length === 1){
        this.error.Month = "*Invalid Card Month"
      }else{
        alert('Confirm');
        this.cardNum = this.seperateInput
        this.cardN = this.CardName 
        this.cardM = this.Month
        this.cardY = this.CardYear
        this.cardC = this.CardCvv
      }

      if(this.CardNumber.length > 16){
        this.CardNumber.slice(0, 17)
        this.error.CardNumber = "*Invalid Card Number"
      } 
      

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
    onlyNumber(){
      this.CardNumber.value = this.CardNumber.value.replace(/[0-9]/g, "");
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
    height: 60vh;
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
  padding: 20px 0;
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
    margin: 7em 0 0 0;
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
    top: 51%;
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
</style>
