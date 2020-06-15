<template>
  <div class="inner">
    <p v-if="currentPage == 'prov'">
      <a
        v-for="(v,prov) in pcasobj"
        :key="prov"
        href="javascript:;"
        @click="ProvClick(prov)"
      >{{prov}}</a>
    </p>
    <p v-if="currentPage == 'city'">
      <a
        v-for="(v,city) in pcasobj[prov]"
        :key="city"
        href="javascript:;"
        @click="CityClick(city)"
      >{{city}}</a>
    </p>
    <p v-if="currentPage == 'area'">
      <a
        v-for="(v,area) in pcasobj[prov][city]"
        :key="area"
        href="javascript:;"
        @click="AreaClick(area)"
      >{{area}}</a>
    </p>
    <p v-if="currentPage == 'street'">
      {{street}}
      <a
        v-for="street in pcasobj[prov][city][area]"
        :key="street"
        href="javascript:;"
        @click="StreetClick(street)"
      >{{street}}</a>
    </p>
    <div class="hd">
      <p>The choosing address:</p>
      <span :class="{'cur': currentPage == 'prov'}" @click="hd_han('prov')">
        <em v-if="prov!=''">{{prov}}</em>
        <em v-else>Please choose a Province</em>
      </span>
      <span v-if="prov!=''" :class="{'cur': currentPage == 'city'}" @click="hd_han('city')">
        <em v-if="city!=''">{{city}}</em>
        <em v-else>Please choose a city</em>
      </span>
      <span v-if="city!=''" :class="{'cur': currentPage == 'area'}" @click="hd_han('area')">
        <em v-if="area!=''">{{area}}</em>
        <em v-else>Please choose a area</em>
      </span>
      <span v-if="area!=''" :class="{'cur': currentPage == 'street'}" @click="hd_han('street')">
        <em v-if="street!=''">{{street}}</em>
        <em v-else>Please choose a street</em>
      </span>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      pcasobj: {},
      //当前显示得界面，值为p,c,a,s
      currentPage: "prov",
      prov: "",
      city: "",
      area: "",
      street: ""
    };
  },
  created() {
    // 拉取接口
    axios.get("http://www.aiqianduan.com:56506/pcas").then(data => {
      this.pcasobj = data.data;
    });
  },
  methods: {
    ProvClick(prov) {
      this.prov = prov;
      // console.log(this.prov)
      this.city = "";
      this.area = "";
      this.street = "";
      this.currentPage = "city";
    },
    CityClick(city) {
      this.city = city;
      this.area = "";
      this.street = "";
      this.currentPage = "area";
    },
    AreaClick(area) {
      this.area = area;
      this.street = "";
      this.currentPage = "street";
    },
    StreetClick(street) {
      this.street = street;
      this.$emit("fulladress", {
        p: this.prov,
        c: this.city,
        a: this.area,
        s: this.street
        
      });
    },
    hd_han(m) {
      this.currentPage = m;
    }
  }
};
</script>

<style lang="less" scoped>
.inner {
  width: 100%;
  height: 100%;
  position: relative;
}
.hd {
  border-top: 1px solid #cccccc;
  width: 700px;
  height: 40px;
  position: absolute;
  left: 0;
  bottom: 0;
  p {
    font-family: "Helvetica Neue", Helvetica, "PingFang SC", "Hiragino Sans GB",
      "Microsoft YaHei", "微软雅黑", Arial, sans-serif;
    font-size: 18px;
    line-height: 26px;
    height: 26px;
    width: 100%;
    font-weight: 600;
  }
  span {
    float: left;
    padding: 0 10px;
    border-bottom: 2px solid #0068ff;
    margin-top: 5px;
    margin-left: 10px;
    font-size: 16px;
    font-weight: 500;
    cursor: pointer;
    font-style: none;

    &.cur {
      background-color: gold;
    }
  }
}
a {
  margin-left: 10px;
  float: left;
}
</style>