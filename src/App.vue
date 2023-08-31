<template>
  <div id="root">
    <div class="todo-container">
      <div class="todo-wrap">
        <!-- 将函数传给子组件 -->
        <MyTop @receive="receive"></MyTop>
        <!-- 给list传递数据 -->
        <MyList
          :todos="todos"
          :checkTodo="checkTodo"
          :dltTodo="dltTodo"
        ></MyList>
        <MyFoot
          :todos="todos"
          @checkAllTodo="checkAllTodo"
          @clearAllTodo="clearAllTodo"
        ></MyFoot>
      </div>
    </div>
  </div>
</template>

<script>
import MyTop from "./components/Top.vue";
import MyFoot from "./components/Foot.vue";
import MyList from "./components/List.vue";
export default {
  name: "App",
  components: {
    MyTop,
    MyList,
    MyFoot,
  },
  data() {
    return {
      todos: [
        {
          id: "01",
          title: "吃饭",
          completed: true,
        },
        {
          id: "02",
          title: "睡觉",
          completed: true,
        },
        {
          id: "03",
          title: "学习",
          completed: false,
        },
      ],
    };
  },
  methods: {
    //添加todo
    receive(e) {
      this.todos.unshift(e);
    },
    //勾选或取消
    checkTodo(id) {
      this.todos.forEach((todo) => {
        if (todo.id == id) {
          todo.completed = !todo.completed;
        }
      });
    },
    //删除
    dltTodo(id) {
      this.todos = this.todos.filter((todo) => todo.id !== id);
    },
    //全选
    checkAllTodo(done) {
      this.todos.forEach((todo) => {
        todo.completed = done;
      });
    },
    //清除
    clearAllTodo() {
      this.todos = this.todos.filter((todo) => {
        return !todo.completed;
      });
    },
  },
  mounted() {
    this.$bus.$on("checkTodo", this.checkTodo);
    this.$bus.$on("dltTodo", this.dltTodo);
  },
  beforeDestroy() {
    this.$bus.$off("checkTod");
    this.$bus.$off("dltTodo");
  },
};
</script>

<style scoped>
/*base*/
body {
  background: #fff;
}

.btn {
  display: inline-block;
  padding: 4px 12px;
  margin-bottom: 0;
  font-size: 14px;
  line-height: 20px;
  text-align: center;
  vertical-align: middle;
  cursor: pointer;
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2),
    0 1px 2px rgba(0, 0, 0, 0.05);
  border-radius: 4px;
}

.btn-danger {
  color: #fff;
  background-color: #da4f49;
  border: 1px solid #bd362f;
}

.btn-danger {
  color: #fff;
  background-color: #da4f49;
  border: 1px solid #5c211e;
}

.btn:focus {
  outline: none;
}

.todo-container {
  width: 600px;
  margin: 0 auto;
}

.todo-container .todo-wrap {
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 5px;
}
</style>
