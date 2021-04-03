<template>
  <div id="main-tab-bar">
    <tab-bar>
      <tab-bar-item path="/home" active-color="pink">
        <template v-slot:item-icon><img src="~assets/img/tabbar/home.svg" alt=""></template>
        <template v-slot:item-icon-active><img src="~assets/img/tabbar/home_active.svg" alt=""></template>
        <template v-slot:item-text><div>首页</div></template>
      </tab-bar-item>

      <tab-bar-item path="/category" active-color="pink">
        <img slot="item-icon" src="~assets/img/tabbar/category.svg" alt="">
        <img slot="item-icon-active" src="~assets/img/tabbar/category_active.svg" alt="">
        <div slot="item-text">分类</div>
      </tab-bar-item>
      <tab-bar-item path="/cart" active-color="pink">
        <img slot="item-icon" src="~assets/img/tabbar/shopcart.svg" alt="">
        <img slot="item-icon-active" src="~assets/img/tabbar/shopcart_active.svg" alt="">
        <div slot="item-text">购物车</div>
      </tab-bar-item>
      <tab-bar-item path="/profile" active-color="pink">
        <img slot="item-icon" src="~assets/img/tabbar/profile.svg" alt="">
        <img slot="item-icon-active" src="~assets/img/tabbar/profile_active.svg" alt="">
        <div slot="item-text">我的</div>
      </tab-bar-item>
    </tab-bar>
  </div>
</template>

<script>
import TabBarItem from "@/components/common/tabbar/TabBarItem";
import TabBar from "@/components/common/tabbar/TabBar";

export default {
  name: "MainTabBar",
  components: {
    TabBarItem,
    TabBar
  },
}
</script>

<style scoped>

</style>
