<template>
  <div class="wrap">
    <!-- 左边得界面 -->
    <div class="nav">
      <ul>
        <li>
          <a href>
            <img src="/images/icon/icon1.svg" alt />
          </a>
        </li>
        <li>
          <a href>
            <img src="/images/icon/icon2.svg" alt />
          </a>
        </li>
        <li>
          <a href>
            <img src="/images/icon/icon3.svg" alt />
          </a>
        </li>
        <li>
          <a href>
            <img src="/images/icon/icon4.svg" alt />
          </a>
        </li>
      </ul>
    </div>
    <!-- 右边得主界面 -->
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
      <!-- 选项卡 -->
      <div class="main">
        <Row :gutter="16">
          <i-col span="8" v-for="(item, index) in addressArr" :key="index">
            <Card :bordered="true" style="height:180px;">
              <div slot="title">
                <b>{{item.alias}}</b>
              </div>
              <div slot="extra">
                <a href>Delete</a>
                <a href>Modify</a>
              </div>
              <p>
                <b>Name:</b>
                {{item.n}}
              </p>
              <p>
                <b>Tel:</b>
                {{item.tel}}
              </p>
              <p>
                <b>Address:</b>
                {{item.p}} {{item.c}} {{item.a}} {{item.s}} {{item.d}}
              </p>
            </Card>
          </i-col>
          <i-col span="8" v-if="addressArr.length != 3">
            <Card :bordered="true" style="height:180px;text-align:center;font-size:100px;">
              <span class="plus" @click="isChoosePCAS = true">+</span>
            </Card>
          </i-col>
        </Row>
      </div>
    </div>
    <!--主界面结束  -->
    <!--弹出层  -->
    <Modal
      v-model="isChoosePCAS"
      width="500"
      title="Add a new shipping address"
      @on-ok="ok"
      @on-cancel="cancel"
    >
      <p>
        <b>
          <span v-if="s ==''">Please Choose your location </span>
          <span v-else>{{p}}{{c}}{{a}}{{s}}</span>
        </b>
         
        
      </p>
      <Dropdown
        trigger="custom"
        :visible="isDropDownvisible"
        style="margin-left: 20px"
        placement="bottom-start"
      >
        <a href="javascript:void(0)" @click="handleDropOpen">
          Province, City, Area, Street
          <Icon type="ios-arrow-down"></Icon>
        </a>
        <DropdownMenu slot="list" style="height:200px; width:600px">
          <div class="dropDownInnerBox">
            <DropdownInner @fulladress="fulladress" />
          </div>
          <div style="text-align: right;margin:10px;">
            <Button type="primary" @click="handleDropClose">关闭</Button>
          </div>
        </DropdownMenu>
      </Dropdown>
    </Modal>
  </div>
</template>

<script>
import axios from "axios";
import DropdownInner from "./components/dropDownInner.vue";
export default {
  data() {
    return {
      // 准备一个空数组
      addressArr: [],
      isChoosePCAS: true,
      isDropDownvisible: true,
      p: "",
      c: "",
      a: "",
      s: ""
    };
  },
  created() {
    // request server data
    axios.get("http://www.aiqianduan.com:56506/shdz/laocai").then(data => {
      // check data.data
      // console.log(data.data)
      this.addressArr = data.data;
    });
  },
  methods: {
    ok() {
      this.$Message.info("Clicked ok");
    },
    cancel() {
      this.$Message.info("Clicked cancel");
    },
    handleDropOpen() {
      this.isDropDownvisible = true;
    },
    handleDropClose() {
      this.isDropDownvisible = false;
    },
    fulladress(obj) {
      this.p = obj.p;
      this.c = obj.c;
      this.a = obj.a;
      this.s = obj.s;
      this.isDropDownvisible= false;
    }
  },
  components: {
    DropdownInner: DropdownInner
  }
};
</script>

<style lang="less" scoped>
.wrap {
  width: 1220px;
  height: 960px;
  margin: 50px auto;
  background-color: #ffffff;
  border-radius: 50px;
  overflow: hidden;
  border: 3px solid #30313c;
}
.nav {
  width: 10%;
  height: 960px;
  float: left;
  background-color: #0068ff;
  border-bottom-left-radius: 50px;
  position: relative;
  ul {
    width: 100%;
    height: 100%;
    list-style: none;
    position: absolute;
    left: 40px;
    top: 190px;
  }
  ul li {
    height: 60px;
    width: 60px;
    margin-bottom: 90px;
  }
  ul li a {
    display: block;
    height: 60px;
    width: 60px;
  }
  ul li img {
    height: 35px;
    width: 35px;
  }
}
.dashboard {
  width: 90%;
  height: 960px;
  float: left;
  h1 {
    height: 60px;
    padding-top: 20px;
    padding-bottom: 60px;
    font-size: 30px;
    line-height: 30px;
    text-align: center;
    font-family: "Gill Sans", "Gill Sans MT", Calibri, "Trebuchet MS",
      sans-serif;
  }
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
  width: 70%;
  height: 760px;
  float: left;
  margin-left: 50px;
  .plus {
    cursor: pointer;
    &:hover {
      color: #0068ff;
    }
  }
}
.dropDownInnerBox {
  height: 150px;
}
</style>