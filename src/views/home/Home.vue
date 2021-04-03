<template>
  <div id="home" class="wrapper">
    <nav-bar class="home-nav"><template v-slot:center>购物街</template></nav-bar>
  </div>
</template>

<script>

import NavBar from "@/components/common/navbr/NavBar";

export default {
  name: "Home",
  components:{
    NavBar
  }
}
</script>
<style scoped>
  .home-nav{
    background-color: var(--color-tint);
    color: #fff;
  }
</style>
