<template>
  <div class="todo-footer" v-show="total">
    <label>
      <input type="checkbox" v-model="isAll" />
    </label>
    <span>
      <span>已完成{{ doneTotal }}</span> / 全部{{ total }}
    </span>
    <button class="btn btn-danger" @click="clearAll">清除已完成任务</button>
  </div>
</template>

<script>
export default {
  name: "MyFooter",
  props: ["todos", "checkAllTodo", "deleteTodo", "clearAllTodo"],
  computed: {
    total() {
      return this.todos.length;
    },
    doneTotal() {
      //forEach方法
      // let i = 0;
      // this.todos.forEach((todo) => {
      //   if (todo.done) i++;
      // });
      // return i;

      //reduce方法
      // return this.todos.reduce((pre, current) => {
      //   return pre + (current.done ? 1 : 0);
      // }, 0);
      return this.todos.reduce(
        (pre, current) => pre + (current.done ? 1 : 0),
        0
      );
    },
    isAll: {
      get() {
        return this.total === this.doneTotal && this.total > 0;
      },
      set(checked) {
        this.checkAllTodo(checked);
      },
    },
  },
  methods: {
    clearAll() {
      // this.todos.forEach((todo) => {
      //   if (todo.done) {
      //     this.deleteTodo(todo.id);
      //   }
      // });
      if (confirm("确定删除已选的吗？")) {
        this.clearAllTodo();
      }
    },
  },
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
