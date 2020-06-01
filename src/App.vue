<template>
  <div class="wrap">
    <h1>二手车市场</h1>
    <Table :columns="className" :data="sCarData"></Table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      className: [
        {
          title: "Name",
          key: "name"
        },
        {
          title: "Age",
          key: "age"
        },
        {
          title: "Address",
          key: "address"
        }
      ],
      sCarData: [
        {
          name: "John Brown",
          age: 18,
          address: "New York No. 1 Lake Park",
          date: "2016-10-03"
        },
        {
          name: "Jim Green",
          age: 24,
          address: "London No. 1 Lake Park",
          date: "2016-10-01"
        },
        {
          name: "Joe Black",
          age: 30,
          address: "Sydney No. 1 Lake Park",
          date: "2016-10-02"
        },
        {
          name: "Jon Snow",
          age: 26,
          address: "Ottawa No. 2 Lake Park",
          date: "2016-10-04"
        }
      ]
    };
  }
};
</script>

<style lang="less" scoped>
.wrap {
  width: 1000px;
  margin: 50px auto;
}
h1 {
  font-size: 30px;
  text-align: center;
}
</style>