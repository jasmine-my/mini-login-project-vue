<template>
  <p>🎉</p>
  <h2 class="header">{{name}}님<br> 회원가입 되었습니다.</h2>

  <ul>
    <li><span>이메일</span>: {{email}}</li>
    <li><span>주소</span>: {{address}}</li>
    <li><span>연락처</span>: {{contract}}</li>
  </ul>
</template>

<script>
export default {
  name: 'OnSuccess',
  props: {
    name: String,
    email: String,
    address: String,
    contract: String
  },
}
</script>

<style scoped>
p{
  text-align: center;
  font-size: 50px;
}
ul > li {
  list-style: none;
  margin-bottom: 10px;
}
span {
  font-weight: bold;
}
</style>