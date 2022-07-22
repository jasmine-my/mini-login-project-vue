<template>
  <h1 class="header">카드 정보</h1>
  <form id="userInfo" action="console.log('통과')" >
    <div class="cardRegiNumWrap">
      <input type="number" v-model="cardRegiNum[0]" @input="(e)=>numberMaxLength4(e.target.value,1)">
      <span>-</span>
      <input type="number" v-model="cardRegiNum[1]" @input="(e)=>numberMaxLength4(e.target.value,2)">
      <span>-</span>
      <input type="number" v-model="cardRegiNum[2]" @input="(e)=>numberMaxLength4(e.target.value,3)">
      <span>-</span>
      <input type="number" v-model="cardRegiNum[3]" @input="(e)=>numberMaxLength4(e.target.value,4) ">
    </div>

    <div class="buttonWrap">
      <div />
      <button class="btn submitBtn" type="submit" @click.prevent="checkForm">완료</button>
    </div>
  </form>
</template>

<script>

export default {
  name: 'CreditCardReginum',
  emits: ['changeCurrentViewSeq'],
  props: {
    currentViewSeq: Number,
  },
  data(){
    return {
      cardRegiNum: [[],[],[],[]],
      isConfirmForm: false
    }
  },
  methods: {
    checkForm: function() {
      const sumArray = (previousValue, currentValue) => {return previousValue + currentValue};
      const fullCardRegiNum = this.cardRegiNum.reduce(sumArray);

      if(fullCardRegiNum.length < 16) {
        this.isConfirmForm = false
      } else {
        let convertCardRegiNum = [];
        [...fullCardRegiNum].reverse().map((value,idx)=>{
          if(idx % 2 === 0){
            const double = value * 2;
            if(double > 9) {
              let answer = 0;
              const stringValue = double.toString();
              for (let i = 0; i < stringValue.length; i++){
                answer += parseInt(stringValue[i]);
              }
              convertCardRegiNum.push(Number(answer))
            } else {convertCardRegiNum.push(Number(double))}
          } else {
            convertCardRegiNum.push(Number(value))
          }
        })

        if(convertCardRegiNum.reduce(sumArray, 0) % 10 === 0) {
          this.isConfirmForm = true;
          this.$emit('changeCurrentViewSeq', 3)
        }
      }
    },
    numberMaxLength4(value,index) {
      const newValue = value.slice(0,4);
      this.cardRegiNum[index - 1] = newValue;
    },
  },
}
</script>

<style scoped>
.cardRegiNumWrap {
  display: grid;
  grid-template-columns: 1fr 0.3fr 1fr 0.3fr 1fr 0.3fr 1fr;
  text-align: center;
  }
.cardRegiNumWrap > input {
  width: 90%
}
</style>