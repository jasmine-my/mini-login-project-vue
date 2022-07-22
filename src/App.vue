<template>
  <div id="myApp">
    <MemberInfo />
    <DeliveryInfo />
    <CreditCardReginum />
  </div>
</template>

<script>
import MemberInfo from "@/components/veiw/memberRegister/MemberInfo";
import DeliveryInfo from "@/components/veiw/memberRegister/DeliveryInfo";
import CreditCardReginum from "@/components/veiw/memberRegister/CreditCardReginum";

export default {
  name: 'App',
  components: {
    CreditCardReginum,
    DeliveryInfo,
    MemberInfo,
  },
  data(){
    return {userName: ''}
  },
}
</script>

<style>
#myApp {
  margin: 0 auto;
  max-width: 500px;
  padding: 10px 50px 30px 50px;
  background: #dae5da;
}

.buttonWrap {
  margin-top: 100px;
  display: flex;
  justify-content: space-between;
}
.btn {
  background: #bebdbd;
  border-radius: 30px;
  padding: 3px 20px;
  border: none;
  transition: all 0.3s;
}
.btn:hover {
  cursor: pointer;
}
.btn.submitBtn {
  background: rgba(66, 185, 131);
  color: white;
}
.btn.submitBtn:is(:hover,:active) {
  background: #308f62;
}
.btn.prevBtn {
  background: indianred;
  color: white;
}
.btn.prevBtn:is(:hover,:active) {
  background: #a95050;
}

</style>
