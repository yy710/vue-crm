<template>
  <div id="app">
    <!--
    <router-link to="/111">1111</router-link>
    <router-link to="/222">222</router-link> 
    -->
    <router-view></router-view>
  </div>
</template>

<script>
import Vue from "vue";
import VueRouter from "vue-router";
import HelloWorld from "./components/HelloWorld.vue";
import NewReferred from "./components/NewReferred.vue";
//const Bar = { template: "<div>bar</div>" };
//const Foo = { template: "<div>foo</div>" };
const routes = [
  {
    path: "/111",
    component: HelloWorld
  },
  {
    path: "/new-referred",
    component: NewReferred
  }
];

Vue.use(VueRouter);

const router = new VueRouter({ routes });

export default {
  name: "app",
  //components: { HelloWorld, NewReferred },
  router
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center; */
  color: #2c3e50;
  /* margin-top: 60px; */
}
</style>
