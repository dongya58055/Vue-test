<template>
  <li>
    <label>
      <input
        type="checkbox"
        :checked="todom.completed"
        @click="handler(todom.id)"
      />
      <span>{{ todom.title }}</span>
    </label>
    <button class="btn btn-danger" @click="dlt(todom.id)" style="">删除</button>
  </li>
</template>

<script>
export default {
  name: "MyItem",
  //申明接受对象
  props: ["todom"],
  methods: {
    handler(id) {
      // this.checkTodo(id)
      this.$bus.$emit("checkTodo", id);
      
    },
    dlt(id) {
      if (confirm("确认删除吗")) {
        //this.dltTodo(id)
        this.$bus.$emit("dltTodo", id);
      }
    },
  },
};
</script>

<style scoped>
/*item*/
li {
  list-style: none;
  height: 36px;
  line-height: 36px;
  padding: 0 5px;
  border-bottom: 1px solid #ddd;
}

li:hover {
  background-color: #ddd;
}
li:hover button {
  display: block;
}

li label {
  float: left;
  cursor: pointer;
}

li label li input {
  vertical-align: middle;
  margin-right: 6px;
  position: relative;
  top: -1px;
}

li button {
  float: right;
  display: none;
  margin-top: 3px;
}

li:before {
  content: initial;
}

li:last-child {
  border-bottom: none;
}

li:hover {
  background: #ddd;
}

li:hover button {
  display: block;
}
</style>