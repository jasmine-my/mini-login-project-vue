<template>
  <h1>배송 정보</h1>
  <form id="userInfo" action="console.log('통과)" >
    <MyInput
        @inputValueChange="userName = $event.target.value"
        :title="'👤 이름'"
        :error-message="'한글 2글자 이상 또는 영문 3글자 이상 입력해주세요'"
        :input-id="'user-name'"
        :input-type="text"
        :is-error="checkIsName"
    />

    <MyInput
        @inputValueChange="userContract = $event.target.value"
        :title="'📞 연락처'"
        :error-message="'비밀번호 형식이 잘못되었습니다'"
        :input-id="'user-password'"
        :input-type="text"
        :is-error="checkIsContract"
    />
    <div>
      <div class="findAddress">
        <span>🏠 주소</span>
        <button type="button" @click="showApi">주소 검색</button>
      </div>
      <input type="text" :value="address.roadAddr" id="address-roadAddr" class="address" disabled>
      <input type="text" :placeholder="'상세주소'" @change="address.detailAddr = $event.target.value" id="address-detailAddr" class="address">
    </div>

    <button id="submitBtn" type="submit" @click.prevent="checkForm">다음</button>
  </form>
</template>

<script>
import MyInput from "@/components/MyInput/MyInput";

export default {
  components: {
    MyInput
  },
  name: 'DeliveryInfo',
  data(){
    return {
      userName: '',
      userContract: '',
      address: {
        zipCode: '',
        roadAddr: '',
        extraAddr: '',
        detailAddr: ''
      },
      confirmForm: false,
      zip: '',
      addr1: '',
      addr2: '',
    }
  },
  methods: {
    checkForm: function() {
      if(this.checkIsName && this.checkIsContract) {
        this.confirmForm = true
      }
    },
    showApi() {
      new window.daum.Postcode({
        oncomplete: (data) => {
          // 팝업에서 검색결과 항목을 클릭했을때 실행할 코드를 작성하는 부분.

          // 도로명 주소의 노출 규칙에 따라 주소를 조합한다.
          // 내려오는 변수가 값이 없는 경우엔 공백('')값을 가지므로, 이를 참고하여 분기 한다.
          let fullRoadAddr = data.roadAddress; // 도로명 주소 변수
          let extraRoadAddr = ''; // 도로명 조합형 주소 변수

          // 법정동명이 있을 경우 추가한다. (법정리는 제외)
          // 법정동의 경우 마지막 문자가 "동/로/가"로 끝난다.
          if (data.bname !== '' && /[동|로|가]$/g.test(data.bname)) {
            extraRoadAddr += data.bname;
          }
          // 건물명이 있고, 공동주택일 경우 추가한다.
          if (data.buildingName !== '' && data.apartment === 'Y') {
            extraRoadAddr += (extraRoadAddr !== '' ? ', ' + data.buildingName : data.buildingName);
          }
          // 도로명, 지번 조합형 주소가 있을 경우, 괄호까지 추가한 최종 문자열을 만든다.
          if (extraRoadAddr !== '') {
            extraRoadAddr = ' (' + extraRoadAddr + ')';
          }
          // 도로명, 지번 주소의 유무에 따라 해당 조합형 주소를 추가한다.
          if (fullRoadAddr !== '') {
            fullRoadAddr += extraRoadAddr;
          }

          // 우편번호와 주소 정보를 해당 필드에 넣는다.
          this.address.zipCode = data.zonecode; //5자리 새우편번호 사용
          this.address.roadAddr = fullRoadAddr;
        }
      }).open()
    },
    computed: {
      checkIsName(){
        const reg_name = /^([가-힣]{2,})|([a-zA-Z]{3,})$/g;
        if(this.userName.length > 0) {
          return reg_name.test(this.userName)
        } else return true;
      },
      checkIsContract(){
        const reg_contract = /^(0+)\d{2,3}[- ]?\d{3,4}[- ]?\d{4}$/g;
        if(this.userContract.length > 0){
          return reg_contract.test(this.userContract);
        } else return true;
      }
    }
  },
}
</script>

<style scoped>
h1 {
  text-align: center;
}
.findAddress {
  display: flex;
  font-weight: 700;
  margin-top: 30px;
  justify-content: space-between;
}
.address {
  width: 70%;
  float: right;
  margin-top: 10px;
  border: 2px solid #2c3e50;
}
</style>