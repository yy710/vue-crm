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

Vue.use(Vant);
Vue.use(Toast);

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