<template>
  <div id="home" class="wrapper">
    <nav-bar class="home-nav"><template v-slot:center>购物街</template></nav-bar>
    <scroll class="content"
            ref="scroll"
            :probe-type="3"
            @scroll="contentScroll"
            @pullingUp="loadMore"
            :pull-up-load="true">
      <home-swiper :banners="banners"/>
      <recommend-view :recommends="recommends"/>
      <FeatureView/>
      <tab-control :titles="['流行', '新款', '精选']"
                   @tabClick="tabClick"
                   ref="tabControl"
                   class="tab-control"
      />
      <goods-list :goods="showGoods"/>
    </scroll>
    <back-top @click.native="backClick" v-show="isShowBackTop"></back-top>



  </div>
</template>

<script>

import HomeSwiper from "./childComps/HomeSwiper";
import RecommendView from "views/home/childComps/RecommendView";
import FeatureView from "views/home/childComps/FeatureView";

import NavBar from "components/common/navbr/NavBar";
import Scroll from "components/common/scroll/Scroll";
import TabControl from "components/content/tabControl/TabControl";
import GoodsList from "components/content/goods/GoodsList";
import BackTop from "components/content/backTop/BackTop";


import {getHomeMultidata, getHomeGoods} from "network/home";

export default {
  name: "Home",
  components:{
    HomeSwiper,
    RecommendView,
    FeatureView,
    NavBar,
    Scroll,
    TabControl,
    GoodsList,
    BackTop
  },
  data(){
    return{
      banners:[],
      recommends:[],
      goods:{
        'pop':{page:0, list:[]},
        'new':{page:0, list:[]},
        'sell':{page:0, list:[]}
      },
      currentType: 'pop',
      isShowBackTop: false,
    }
  },
  created(){
    // 1.请求多个数据
    this.getHomeMultidata()

    //2请求推荐商品数据
    this.getHomeGoods('pop')
    this.getHomeGoods('new')
    this.getHomeGoods('sell')
  },

  computed:{
    showGoods(){
      return this.goods[this.currentType].list
    }
  },

  methods:{
    /**
     *
     * 网络请求祥相关犯法
     * */
    getHomeMultidata(){
      getHomeMultidata().then(res => {
        this.banners = res.data.banner.list;
        this.recommends = res.data.recommend.list
        // console.log(res);
      })
    },
    getHomeGoods(type){
      const page = this.goods[type].page + 1
       getHomeGoods(type, page).then(res => {
          this.goods[type].list.push(...res.data.list);
          this.goods[type].page += 1;

       })
    },

    /**
     *
     * 事件监听相关方法
     */
    tabClick(index){
      switch (index){
        case 0:
          this.currentType = 'pop';
          break
        case 1:
          this.currentType = 'new'
          break
        case 2:
          this.currentType = 'sell'
          break
      }
    },
    contentScroll(position){
      this.isShowBackTop = -position.y > 1000
    },
    loadMore(){
      this.getHomeGoods(this.currentType)
    },
    backClick(){
      this.$refs.scroll.scrollTo(0,0);
    }
  }
}
</script>
<style scoped>
  .home-nav{
    background-color: var(--color-tint);
    color: #fff;

    position: fixed;
    left: 0;
    right: 0;
    top: 0;
    z-index: 9;
  }
  #home{
    /*padding-top: 44px;*/
    position: relative;
    height: 100vh;
  }
  .tab-control{
    position: sticky;
    top: 44px;
    z-index: 9;
  }
  .content{
    overflow: hidden;

    position: absolute;
    top: 44px;
    bottom: 49px;
    left: 0;
    right: 0;
  }

</style>
