<template>
  <div id="myApp">
<!--    <MemberInfo />-->
    <DeliveryInfo />
  </div>
</template>

<script>
// import MemberInfo from "@/components/veiw/memberRegister/MemberInfo";
import DeliveryInfo from "@/components/veiw/memberRegister/DeliveryInfo";

export default {
  name: 'App',
  components: {
    DeliveryInfo,
    // MemberInfo,
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

#submitBtn {
  margin-top: 100px;
  background: rgba(66, 185, 131);
  border-radius: 30px;
  padding: 3px 20px;
  color: white;
  border: none;
}
#submitBtn:is(:hover,:active,:focus) {
  background: #308f62;
  transition: all 0.3s;
}

</style>
