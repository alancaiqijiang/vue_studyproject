<template>
  <!-- 模态框弹出层 -->
  <div>
    <div>
      <Form ref="myform" :model="myform" :rules="ruleValidate" :label-width="180">
        <FormItem label="Please choose Address." prop="pcas">
          <div>
            <span v-if="s ==''">Please Choose your location</span>
            <span v-else>{{p}} {{c}} {{a}} {{s}}</span>
          </div>
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
            <DropdownMenu slot="list" style="height:220px; width:600px">
              <div class="dropDownInnerBox">
                <DropdownInner @fulladress="fulladress" />
              </div>
              <div style="text-align: right;margin:10px;">
                <Button type="primary" @click="handleDropClose">关闭</Button>
              </div>
            </DropdownMenu>
          </Dropdown>
        </FormItem>
        <FormItem label="Phone No." prop="tel">
          <i-input v-model="myform.tel" placeholder="Please Enter your Telephone Number"></i-input>
        </FormItem>
        <FormItem label="Address Detail" prop="d">
          <i-input v-model="myform.d" placeholder="Please Enter your detail address"></i-input>
        </FormItem>
        <FormItem label="Name" prop="n">
          <i-input v-model="myform.d" placeholder="Please Enter your detail address"></i-input>
        </FormItem>
        <FormItem label="address tag" prop="alias">
          <Row>
            <i-col span="8">
              <i-input v-model="myform.alias" placeholder="address tag"></i-input>
            </i-col>
            <i-col span="24-8">
                <Button v-for="(item,index) in ['家','公司','父母家']" :key="index" @click="aliasbtn(item)">
                    {{item}}
                </Button>
            </i-col>
          </Row>
        </FormItem>
      </Form>
    </div>
  </div>
  <!-- 模态框弹出层结束 -->
</template>

<script>
import DropdownInner from "./dropDownInner.vue";

export default {
  data() {
    return {
      // 准备一个空数组
      isChoosePCAS: true,
      isDropDownvisible: false,
      p: "",
      c: "",
      a: "",
      s: "",
      // 增加一个校验规则
      ruleValidate: {
        pcas: [
          // 检查是否填写
          {
            required: true
          }
        ],
        d: [
          // 检查是否填写
          {
            required: true,
            message: "please enter your street, house and room number",
            min: 5,
            max: 40
          }
        ],
        n: [
          // 检查是否填写
          {
            required: true,
            message: "please enter your Name",
            min: 5,
            max: 40
          }
        ],
        alias: [
          // 检查是否填写
          {
            required: true,
            message: "please enter your address tag",
          }
        ],
        tel: [
          // 检查是否填写
          {
            required: true,
            message: "The phone number cannot be empty",
            trigger: "blur"
          },
          // 检查是否输入11位号码
          {
            pattern: /^(13[0-9]|14[579]|15[0-3,5-9]|16[6]|17[0135678]|18[0-9]|19[89])\d{8}$/,
            message: "please enter Validated phone number",
            trigger: "blur"
          }
        ]
      },
      // 与电话表单双向绑定
      myform: {
        tel: "",
        d: "",
        n: "",
        alias: ""
      }
    };
  },
  components: {
    DropdownInner
  },
  methods: {
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
      this.isDropDownvisible = false;
    },
    aliasbtn(tag){
        this.$set(this.myform,'alias',tag)
    }
  }
};
</script>

<style lang="less" scoped>
.dropDownInnerBox {
  height: 170px;
}
</style>