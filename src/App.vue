<template>
  <div id="myApp">
    <MemberInfo v-if="currentViewSeq === 0" @changeCurrentViewSeq="changeCurrentViewSeq" @setEmail="setEmail"/>
    <DeliveryInfo v-if="currentViewSeq === 1" @changeCurrentViewSeq="changeCurrentViewSeq" @setName="setName" @setContract="setContract" @setAddress="setAddress"/>
    <CreditCardReginum v-if="currentViewSeq === 2" @changeCurrentViewSeq="changeCurrentViewSeq"/>
    <OnSuccess v-if="currentViewSeq === 3" :name="name" :email="email" :address="address" :contract="contract" />
  </div>
</template>

<script>
import MemberInfo from "@/components/veiw/memberRegister/MemberInfo";
import DeliveryInfo from "@/components/veiw/memberRegister/DeliveryInfo";
import CreditCardReginum from "@/components/veiw/memberRegister/CreditCardReginum";
import OnSuccess from "@/components/veiw/memberRegister/OnSuccess";

export default {
  name: 'App',
  components: {
    OnSuccess,
    CreditCardReginum,
    DeliveryInfo,
    MemberInfo,
  },
  data(){
    return {
      currentViewSeq: 0,
      name: '',
      email: '',
      address: '',
      contract: ''
    }
  },
  methods: {
    changeCurrentViewSeq: function(seq) {
      this.currentViewSeq = seq;
    },
    setName: function(name) {
      this.name = name;
    },
    setEmail: function(email) {
      this.email = email;
    },
    setAddress: function(address) {
      this.address = address;
    },
    setContract: function(contract) {
      this.contract = contract;
    },
  }
}
</script>

<style>
#myApp {
  margin: 0 auto;
  max-width: 500px;
  padding: 10px 50px 30px 50px;
  background: #dae5da;
}

.header {
  text-align: center;
  margin-bottom: 100px;
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
