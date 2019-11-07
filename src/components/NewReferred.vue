<template>
  <div>
    <van-cell-group>
      <van-field
        v-model="customerName"
        required
        label="客户姓名"
        left-icon="contact"
        placeholder="请输入客户姓名"
      ></van-field>
      <van-field
        v-model="customerPhone"
        required
        label="客户手机号"
        placeholder="请输入客户手机号"
        left-icon="phone-o"
      ></van-field>
      <van-cell>
        <van-button type="default" @click="sendNewReferred">send</van-button>
      </van-cell>
    </van-cell-group>
  </div>
</template>

<script>
import Vue from "vue";
import Vant from "vant";
import axios from "axios";
import "vant/lib/index.css";

Vue.use(Vant);

export default {
  name: "NewReferred",
  data() {
    return {
      customerName: null,
      customerPhone: null
    };
  },
  props: {
    employer: Object
  },
  methods: {
    sendNewReferred() {
      axios
        .get("http://www.all2key.cn/oa.html")
        .then(r => window.console.log("axios return: ", r))
        .catch(err => window.console.log("error!", err));
    }
  }
};
</script>

<style>
</style>