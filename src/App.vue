<template>
  <div class="wrap">
    <div class="dashboard">
      <h1>Billing Address</h1>
      <div class="sider-bar">
        <ul>
          <li>
            <a href>Perosonal Info</a>
          </li>
          <li>
            <a href>Perosonal Info</a>
          </li>
          <li>
            <a href>Perosonal Info</a>
          </li>
          <li>
            <a href>Perosonal Info</a>
          </li>
        </ul>
      </div>
      <div class="main">
        <Row :gutter="16">
          <i-col span="8">
            <Card :bordered="true">
                <p slot="title">card</p>
                <p>Content of card</p>
                <p>Content of card</p>
                <p>Content of card</p>
            </Card>
          </i-col>
          <i-col span="8">
            <Card :bordered="true">
                <p slot="title"> card</p>
                <p>Content of card</p>
                <p>Content of card</p>
                <p>Content of card</p>
            </Card>
          </i-col>
          <i-col span="8">
            <Card :bordered="true">
                <p slot="title">card</p>
                <p>Content of card</p>
                <p>Content of card</p>
                <p>Content of card</p>
            </Card>
          </i-col>
        </Row>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      // 准备一个空数组
      addressArr: []
    };
  },
  created() {
    // request server data
    axios.get("http://www.aiqianduan.com:56506/shdz/laocai").then(data => {
      // check data.data
      // console.log(data.data)
      this.addressArr = data.data;
    });
  }
};
</script>

<style lang="less" scoped>
.wrap {
  width: 1020px;
  height: 960px;
  margin: 50px auto;
  background-color: #1d212a;
  border-radius: 50px;
}
.dashboard {
  width: 1020px;
  height: 180px;
}
.sider-bar {
  width: 20%;
  height: 760px;
  float: left;
  border-right: 2px solid #abafba;
  position: relative;
  ul {
    list-style: none;
    position: absolute;
    top: 100px;
    left: 40px;
  }
  ul li {
    height: 40px;
    width: 120px;
    line-height: 40px;
    margin-top: 80px;
    font-family: "Gill Sans", "Gill Sans MT", Calibri, "Trebuchet MS",
      sans-serif;
    font-size: 18px;
  }
  ul li a {
    display: block;
    width: 120px;
    text-align: center;
  }
}
.main {
  width: 80%;
  height: 760px;
  float: left;
}
h1 {
  padding-top: 20px;
  font-size: 30px;
  line-height: 30px;
  text-align: center;
  color: white;
  font-family: "Gill Sans", "Gill Sans MT", Calibri, "Trebuchet MS", sans-serif;
}
</style>