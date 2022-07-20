<template>
  <MemberInfo />
</template>

<script>
import MemberInfo from "@/components/veiw/memberRegister/MemberInfo";

export default {
  name: 'App',
  components: {
    MemberInfo,
  },
  data(){
    return {userName: ''}
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
