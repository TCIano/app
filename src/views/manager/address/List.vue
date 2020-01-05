<template>
  <div>
    <briup-fulllayout title="常用地址">
      <!-- {{addresses}} -->
      {{info}}
      <van-list>
        <van-cell
          v-for="item in addresses"
          :key="item.id"
          :title="item.province+' '+item.city+' '+item.area+' '+item.address"
        />
      </van-list>
      <van-button  block type="defaul" @click="toAddressEditHandler">添加</van-button>
    </briup-fulllayout>
  </div>
</template>

<script>
import {mapState} from "vuex";

import {get} from "../../../http/axios"
export default {
  data() {
    return {
      addresses: []
    };
  },
  computed:{
      //将状态机中的user对象 中的info对象获取到
      ...mapState("user",["info"])
      },
  created() {
    this.loadAddress();
  },
  methods: {
      //跳转到编辑地址
      toAddressEditHandler(){
          //编辑跳转,跳转到编辑页面
          this.$router.push("/manager/address_edit");
      },
    //加载地址
    loadAddress() {
        let id  = this.info.id;
      let url = "/address/findByCustomerId?id=" + id;
      get(url).then(response => {
        this.addresses = response.data;
      });
    }
  }
};
</script>