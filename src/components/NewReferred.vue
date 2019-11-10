<template>
  <div>
    <van-nav-bar
      title="录入新的转介绍信息"
      left-text="取消"
      right-text="保存"
      left-arrow
      @click-left="onClickLeft"
      @click-right="onClickRight"
    />
    <van-cell-group title="请输入客户信息(必填)：">
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
    </van-cell-group>
    <van-radio-group v-model="source">
      <van-cell-group title="请选择信息来源：">
        <van-cell title="来源 1" clickable @click="radio = '1'">
          <van-radio slot="right-icon" name="1" />
        </van-cell>
        <van-cell title="来源 2" clickable @click="radio = '2'">
          <van-radio slot="right-icon" name="2" />
        </van-cell>
      </van-cell-group>
    </van-radio-group>
    <van-cell-group title="请输入介绍人信息：">
      <van-field v-model="fromName" label="介绍人姓名" placeholder="请输入介绍人姓名"></van-field>
      <van-field v-model="fromPhone" label="介绍人手机号" placeholder="请输入介绍人手机号"></van-field>
    </van-cell-group>
    <van-cell>
      <van-button type="primary" style="width: 100%" @click="sendNewReferred">确认保存</van-button>
    </van-cell>
  </div>
</template>

<script>
import Vue from "vue";
import Vant from "vant";
import { Toast } from "vant";
import axios from "axios";
import "vant/lib/index.css";

const aaa = 1;

Vue.use(Vant);
Vue.use(Toast);

wx.config({
    beta: true,// 必须这么写，否则wx.invoke调用形式的jsapi会有问题
    debug: true, // 开启调试模式,调用的所有api的返回值会在客户端alert出来，若要查看传入的参数，可以在pc端打开，参数信息会通过log打出，仅在pc端时才会打印。
    appId: 'ww29233ad949e808bf', // 必填，企业微信的corpID
    timestamp: new Date().getTime(), // 必填，生成签名的时间戳
    nonceStr: 'kmyzcrm', // 必填，生成签名的随机串
    signature: '',// 必填，签名，见 附录-JS-SDK使用权限签名算法
    jsApiList: [] // 必填，需要使用的JS接口列表，凡是要调用的接口都需要传进来
});


export default {
  name: "NewReferred",
  data() {
    return {
      customerName: null,
      customerPhone: null,
      source: 2,
      fromName: null,
      fromPhone: null
    };
  },
  props: {
    employer: Object
  },
  methods: {
    onClickLeft() {
      Toast("返回");
    },
    onClickRight() {
      this.sendNewReferred()
        .then(() => Toast.success("保存成功！"))
        .catch(() => Toast.fail("保存失败！"));
    },
    sendNewReferred() {
      //window.console.log(this.$data);
      return axios
        .get("http://localhost:8000/yz/referred/new", {
          params: {
            customerName: this.customerName,
            customerPhone: this.customerPhone,
            source: this.source,
            fromName: this.fromName,
            fromPhone: this.fromPhone
          }
        })
        .then(r => window.console.log("axios return: ", r.data))
        .catch(err => window.console.log("error!", err));
    }
  }
};
</script>

<style>
</style>