<template>
  <div class="home">
    <header class="header">
      <img src="../../assets/home.jpg" alt="" />
    </header>
    <div>
      <!-- 分类 value in  里面是导航里面的数组 即所要调用哪个里面的数据-->
      <van-grid :column-num="3">
        <van-grid-item v-for= "value in categories" :key= "value.id" :icon= "value.icon" :text= "value.name" />
      </van-grid>
      <!-- 产品 -->
      <van-grid :column-num="1" icon-size="700px">
        <van-grid-item v-for= "value in products" :key= "value.id" :icon= "value.photo" :text= "value.name" />
      </van-grid>
  {{products}}
    </div>
    
  </div>
</template>

<script>
import {get,post} from '../../http/axios';
import { mapState, mapActions } from "vuex";
export default {
  data(){
    return{
      categories:[],
      products:[]
    }
  },
  created() {
    this.loadCategories();
    this.locdProducts();
  },
  methods: {

    loadCategories(){
      let url = "/category/findAll"
      get(url).then((response)=>{
        this.categories = response.data.slice(0,6);
      })
    },
    //加载产品信息
    locdProducts(){ 
      let url = "/product/query"
      let params = {
        page:0,
        pageSize:10
      }
      post(url,params).then((response)=>{
        this.products = response.data.list;
      })
    },
  }
};
</script>

<style scoped>
.home {
  padding-bottom: 50px;
}
.header {
  height: 300px;
  overflow: hidden;
}
.header img {
  width: 100%;
}
</style>