<template>
  <!--隐式类型转换-->
  <div class="todo-footer" v-show="todos.length">
    <label>
      <!--这里也可用v-model来替代，此时不需要计算属性了-->
      <!--      <input type="checkbox" :checked="isAll" @change="checkAll"/>-->
      <input
        type="checkbox"
        :checked="doneTotal === todos.length && todos.length > 0"
        @click="checkAll"
      />
    </label>
    <span>
      <span>已完成{{ doneTotal }}</span> / 全部{{ todos.length }}
    </span>
    <button class="btn btn-danger" @click="clearAll">清除已完成任务</button>
  </div>
</template>

<script>
export default {
  name: "MyFoot",
  props: ["todos"],
  computed: {
    doneTotal() {
      /*
        this.todos.reduce((pre,current)=>{
            return per+(current.completed?1:0)
        },0)
        */
      let i = 0;
      this.todos.forEach((todo) => {
        if (todo.completed) i++;
      });
      return i;
    },
  },
  methods:{
    checkAll(e){
        this.$emit('checkAllTodo',e.target.checked)
    },
    clearAll(){
        this.$emit('clearAllTodo')
    }
  }
};
</script>

<style scoped>
/*footer*/
.todo-footer {
  height: 40px;
  line-height: 40px;
  padding-left: 6px;
  margin-top: 5px;
}

.todo-footer label {
  display: inline-block;
  margin-right: 20px;
  cursor: pointer;
}

.todo-footer label input {
  position: relative;
  top: -1px;
  vertical-align: middle;
  margin-right: 5px;
}

.todo-footer button {
  float: right;
  margin-top: 5px;
}
</style>