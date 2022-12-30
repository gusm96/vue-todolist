<template>
  <div id="app">
    <todo-header></todo-header>
    <todo-input @addTodoItem="addOneItem"></todo-input>
    <todo-list
      v-bind:propsdata="todoItems"
      @removeItem="removeOneItem"
      @toggleItem="toggleOneItem"
    ></todo-list>
    <todo-footer @clearAll="clearAllItems"></todo-footer>
  </div>
</template>

<script>
import TodoHeader from "./components/TodoHeader.vue";
import TodoInput from "./components/TodoInput.vue";
import TodoList from "./components/TodoList.vue";
import TodoFooter from "./components/TodoFooter.vue";

export default {
  name: "app",
  data() {
    return {
      todoItems: []
    };
  },
  created() {
    if (localStorage.length > 0) {
      for (var i = 0; i < localStorage.length; i++) {
        if (localStorage.key(i) !== "loglevel:webpack-dev-server") {
          this.todoItems.push(
            JSON.parse(localStorage.getItem(localStorage.key(i)))
          );
        }
      }
    }
  },
  components: {
    TodoHeader,
    TodoInput,
    TodoList,
    TodoFooter
  },
  methods: {
    addOneItem: function(todoItem) {
      const obj = {
        completed: false,
        item: todoItem
      };
      localStorage.setItem(todoItem, JSON.stringify(obj));
      this.todoItems.push(obj);
      console.log(JSON.stringify(obj));
    },
    removeOneItem: function(todoItem, index) {
      var yesNo = confirm("정말로 삭제하시겠습니까?");
      // 실수로 delete 방지
      if (yesNo == true) {
        localStorage.removeItem(todoItem.item);
        this.todoItems.splice(index, 1);
      }
    },
    toggleOneItem: function(todoItem, index) {
      this.todoItems[index].completed = !this.todoItems[index].completed;
      // localStorage 에서 update 할 수 있는 API 가 없기 때문에
      // removeItem 으로 삭제 후 다시 setItem 을 해준다.
      // localStorage 갱신 하는 방법
      localStorage.removeItem(todoItem.item);
      localStorage.setItem(todoItem.item, JSON.stringify(todoItem));
    },
    clearAllItems: function() {
      const yesNo = confirm("정말로 모두 삭제하시겠습니까?");
      if (yesNo) {
        localStorage.clear();
        this.todoItems = [];
      }
    }
  }
};
</script>

<style>
body {
  text-align: center;
  background-color: #f6f6f6;
  display: flex;
  align-items: center;
  justify-content: center;
}
input {
  border-style: groove;
  width: 200px;
}
button {
  border-style: groove;
}
.shadow {
  box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03);
}
</style>
