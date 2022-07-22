<template>
  <h1 class="header">개인 정보</h1>
  <form id="userInfo" >
    <MyInput
        @inputValueChange="userEmail = $event.target.value"
        :title="'📧 이메일'"
        :error-message="'이메일 형식이 잘못되었습니다'"
        :input-id="'user-email'"
        :input-type="'email'"
        :is-error="checkIsEmail"
    />

    <MyInput
        @inputValueChange="userPW = $event.target.value"
        :title="'🔑비밀번호'"
        :error-message="'비밀번호 형식이 잘못되었습니다'"
        :input-id="'user-password'"
        :input-type="'text'"
        :is-error="checkIsPW"
    />

    <MyInput
        @inputValueChange="userConfirmPW = $event.target.value"
        :title="'✔비밀번호 확인'"
        :error-message="'비밀번호와 일치하지 않습니다'"
        :input-id="'user-confirm-password'"
        :input-type="'text'"
        :is-error="checkIsConfirmPW"
    />
    <div class="buttonWrap">
      <div />
      <button class="btn submitBtn" type="submit" @click.prevent="checkForm">다음</button>
    </div>
  </form>
  </template>

<script>
import MyInput from "@/components/MyInput/MyInput";

export default {
  components: {
    MyInput
  },
  name: 'MemberInfo',
  emits: ['changeCurrentViewSeq', 'setEmail'],
  data(){
    return {
      userEmail: '',
      userPW: '',
      userConfirmPW: '',
      isConfirmForm: false,
    }
  },
  methods: {
    checkForm: function() {
      if(this.checkIsEmail && this.checkIsPW && this.checkIsConfirmPW) {
          this.isConfirmForm = true;
          this.$emit('changeCurrentViewSeq', 1);
          this.$emit('setEmail', this.userEmail);
      }
    }
  },
  computed: {
    checkIsEmail(){
      const reg_email = /^([0-9a-zA-Z_-]+)@([0-9a-zA-Z_-]+)(\.[0-9a-zA-Z_-]+){1,2}$/;
      if(this.userEmail.length > 0) {
        return reg_email.test(this.userEmail)
      } else return false;
    },
    checkIsPW(){
      const reg_pw = /^(?=.*[a-z])(?=.*[A-Z])(?=.*[$@!#%*?&])[A-Za-z$@#!%*?&]{8,}$/;
      if(this.userPW.length > 0){
        return reg_pw.test(this.userPW);
      } else return false;
    },
    checkIsConfirmPW(){
      const reg_pw = /^(?=.*[a-z])(?=.*[A-Z])(?=.*[$@!#%*?&])[A-Za-z$@#!%*?&]{8,}$/;
      if(this.userConfirmPW.length > 0) {
        return reg_pw.test(this.userConfirmPW) && (this.userConfirmPW === this.userPW);
      } else return false;
    },
  }
}
</script>

<style scoped>
</style>