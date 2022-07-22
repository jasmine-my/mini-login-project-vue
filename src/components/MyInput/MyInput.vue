<template>
  <div class="inputWrap">
    <div class="inputBox">
      <label v-if="title" >{{title}} </label>
      <input :type="inputType"
             @input="$emit('inputValueChange', $event)" />
    </div>
    {{inputType}}
    <span class="errorMessage" v-if="!isError">{{errorMessage}}</span>
  </div>
</template>

<script>
export default {
  name: 'MyInput',
  emits: ['inputValueChange'],
  props: {
    title: String,
    inputType: String,
    inputId: String,
    errorMessage: String,
    isError: Boolean,
    placeholder: String
  },
  data(){
    return {
      inputValue: ''
    }
  },
}
</script>

<style scoped>
  input {
    border: 2px solid #2c3e50;
  }
  input:is(:active, :hover, :focus) {
    border-color: #42b983;
    transition: all 0.3s;
  }
  input::-webkit-outer-spin-button,
  input::-webkit-inner-spin-button {
    -webkit-appearance: none;
    margin: 0;
  }

  label {
    font-weight: 700;
  }
  .inputWrap {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: start;
    margin-top: 30px;
  }
  .inputBox {
    display: grid;
    width: 100%;
    grid-template-columns: 30% 70%;
  }
  .errorMessage {
    color: indianred;
    display: inline-block;
    margin-top: 10px;
  }
</style>