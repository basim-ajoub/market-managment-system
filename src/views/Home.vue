<template>
  <div class="home">
   <h1 class="head-title">Dreams Market</h1>
    <Boxes />
    <HomeChart />
  </div>
</template>

<script>
// @ is an alias to /src
import Boxes from "../components/home/boxCom.vue";
import HomeChart from "../components/home/dailycharts.vue";

export default {
  name: "Home",
  components: {
    Boxes,HomeChart,
  },
};
</script>
<style lang="scss">
$permanentFont: "Permanent Marker", cursive;
$kashenFont: "Kaushan Script", cursive;
$meriendaFont: "Merienda", cursive;
$luckiestFont: "Luckiest Guy", cursive;
.home{
  width: 100%;
  height: 98.4%;
  padding-top: 10px;
  .head-title{
    margin-left: 1%;
    margin-bottom: 40px;
    font-family: $kashenFont;
    letter-spacing: 1px;
    
  }
}
</style>
