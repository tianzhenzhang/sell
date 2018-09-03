<template>
  <div id="app">
    <v-header :seller="seller"></v-header>
    <div class="tab">
      <div class="tab-item">
        <!-- <a v-link="{path:'/goods'}">商品</a> -->
        <router-link to="/goods">商品</router-link>
      </div>
      <div class="tab-item">
        <!-- <a v-link="{path:'/ratings'}">评价</a> -->
        <router-link to="/ratings">评价</router-link>
      </div>
      <div class="tab-item">
        <!-- <a v-link="{path:'/seller'}">商家</a> -->
        <router-link to="/seller">商家</router-link>
      </div>
    </div>
    <!-- <div class="content">
      I am content
    </div> -->
    <router-view></router-view>
  </div>
</template>

<script>
import header from "./components/header/header";
// import axios from 'axios';

const ERR_OK = 0;

export default {
    name: 'App',
    components: {
        'v-header': header
    },
    data () {
        return {
        seller: {}
        }
    },
    created () {
        this.$http.get('/api/seller').then(res => {
        if(res.data.errno === ERR_OK){
            console.log(res.data.data);
            this.seller = res.data.data;
        }
        }).catch(err => {
        console.log(err);
        })
    }
}
</script>

<style lang="stylus">
  @import './common/stylus/mixin.styl';

  #app 
    .tab{
      display: flex;
      display: -webkit-flex;
      width: 100%;
      height: 40px;
      line-height: 40px;
      border-1px(rgba(7,17,27,0.1));
      // position: relative;
      .tab-item {
        flex: 1;
        text-align: center;
        & > a {
          display: block;
          font-size: 14px;
          color: rgb(77,85,93);
          text-decoration: none;
          &.active{
            color: rgb(240,20,20);
          } 
        }                  
      }
      // &:after{
      //   display: block;
      //   position: absolute;
      //   left: 0;
      //   bottom: 0;
      //   width: 100%;
      //   border-top: 1px solid rgba(7,17,27,0.1);
      //   content: "";
      // }      
    }   
</style>
