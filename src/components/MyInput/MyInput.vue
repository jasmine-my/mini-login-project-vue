<template>
  <div class="inputWrap">
    <h3 v-if="title">{{title}}: </h3>
    <input type="text"
           id="inputId" @input="$emit('inputValueChange', $event)"
    />
  </div>
  <p v-if="!isError">{{errorMessage}}</p>
</template>

<script>
export default {
  name: 'MyInput',
  props: {
    title: String,
    inputId: String,
    errorMessage: String,
    isError: Boolean
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
  }
  .inputWrap {
    display: flex;
    justify-content: center;
    align-items: center;
  }
</style>