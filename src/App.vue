<template>
  <div id="app">
    <div>
      <span>姓名:</span>
      <input
        type="text"
        placeholder="姓名"
        v-model="name"
      />
    </div>
    <div>
      <span>年龄:</span>
      <input
        type="text" 
        placeholder="年龄"
        v-model.number="age"
      />
    </div>
    <div>
      <span>性别:</span>
      <select>
        <option value="男">男</option>
        <option value="女">女</option>
      </select>
    </div>
    <div>
      <button @click.prevent="addFn">添加/修改</button>
    </div>
    <div>
      <table border="1" cellpadding="10" cellspacing="0">
        <tr>
          <th>序号</th>
          <th>姓名</th>
          <th>年龄</th>
          <th>性别</th>
          <th>操作</th>
        </tr>
        <tr v-for="obj in list" :key="obj.id">
          <td>{{ obj.id }}</td>
          <td>{{ obj.name }}</td>
          <td>{{ obj.age }}</td>
          <td>{{ obj.sex }}</td>
          <td>
            <button @click="delFn(obj.id)">删除</button>
            <button>编辑</button>
          </td>
        </tr>
      </table>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      list: [
        { id: 1, name: "tom", age: 19, sex: "男" },
        { id: 2, name: "jone", age: 21, sex: "女" },
      ],
      name: "",
      age: 0,
      sex: "男",
    };
  },
  methods: {
    addFn() {
      // 5. 判断是否为空
      if (this.name.trim().length == 0 || this.age == 0) {
        this.name = "";
        this.age = 0;
        return alert("请输入完整的信息");
      }
      // 3. 把值以对象形式-插入list
      this.list.push({
        // 当前数组最后一个对象的id+1作为新对象id值
        id: this.list[this.list.length - 1].id + 1,
        name: this.name,
        age: this.age,
        sex,
      });
      // 清空输入的值
      this.name = "";
      this.age = 0;
    },
    delFn(id) {
      let index = this.list.findIndex((obj) => obj.id === id);
      this.list.splice(index, 1);
    },
  },
};
</script>
