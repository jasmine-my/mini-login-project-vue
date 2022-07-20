<template>
  <!--      TODO-->
  <h1>개인 정보</h1>
  <MyInput
      @inputValueChange="userEmail = $event.target.value"
      :title="'이메일'"
      :error-message="'이메일 형식이 잘못되었습니다'"
      :input-id="'user-email'"
      :is-error="isEmail"
  />
  {{isEmail}}
  <p>메일 주소:{{userEmail}}</p>

  <MyInput
      @inputValueChange="userPW = $event.target.value"
      :title="'비밀번호'"
      :error-message="'비밀번호 형식이 잘못되었습니다'"
      :input-id="'user-password'"
      :is-error="false"
  />
  <MyInput
      @inputValueChange="userConfirmPW = $event.target.value"
      :title="'비밀번호 확인'"
      :error-message="'비밀번호와 일치하지 않습니다'"
      :input-id="'user-confirm-password'"
      :is-error="this.userConfirmPW === this.userPW"
  />
</template>

<script>

import MyInput from "@/components/MyInput/MyInput";

export default {
  components: {
    MyInput
  },
  name: 'MemberInfo',
  data(){
    return {
      userEmail: '',
      isEmail: this.checkIsEmail(this.userEmail),
      userPW: '',
      userConfirmPW: '',
    }
  },
  methods: {
    checkIsEmail: (v) => {
      const reg_email = /^([0-9a-zA-Z_-]+)@([0-9a-zA-Z_-]+)(\.[0-9a-zA-Z_-]+){1,2}$/;
      return reg_email.test(v);
    }
  }
}
</script>

<style scoped>
div {
  margin-top: 10px;
  border-radius: 5px;
  background: antiquewhite;
}
</style>