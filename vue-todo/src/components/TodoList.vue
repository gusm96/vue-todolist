<template>
  <main>
    <div>
      <ul>
        <li v-for="(todoItem, index) in todoItems" v-bind:key="todoItem.item">
          <i
            class="checkBtn fas fa-check"
            v-bind:class="{ checkBtnCompleted: todoItem.completed }"
            @click="toggleComplete(todoItem, index)"
          ></i>
          <span v-bind:class="{ textCompleted: todoItem.completed }">{{
            todoItem.item
          }}</span>
          <span class="removeBtn" v-on:click="removeTodo(todoItem, index)">
            <i class="fas fa-trash-alt" />
          </span>
        </li>
      </ul>
    </div>
  </main>
</template>
<script>
export default {
  name: "TodoList",
  components: {},
  data() {
    return {
      todoItems: []
    };
  },
  beforeCreate() {},
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
  beforeMount() {},
  mounted() {},
  beforeUpdate() {},
  updated() {},
  beforeUnmount() {},
  unmounted() {},
  methods: {
    removeTodo: function(todoItem, index) {
      var yesNo = confirm("정말로 삭제하시겠습니까?");
      // 실수로 delete 방지
      if (yesNo == true) {
        localStorage.removeItem(todoItem.item);
        this.todoItems.splice(index, 1);
      }
    },
    toggleComplete: function(todoItem, index) {
      todoItem.completed = !todoItem.completed;
      // localStorage 에서 update 할 수 있는 API 가 없기 때문에
      // removeItem 으로 삭제 후 다시 setItem 을 해준다.
      // localStorage 갱신 하는 방법
      localStorage.removeItem(todoItem.item);
      localStorage.setItem(todoItem.item, JSON.stringify(todoItem));
    }
  }
};
</script>
<style scoped>
ul {
  list-style-type: none;
  padding-left: 0px;
  margin-top: 0;
  text-align: left;
}
li {
  display: flex;
  min-height: 50px;
  height: 50px;
  line-height: 50px;
  margin: 0.5rem 0;
  padding: 0 0.9rem;
  background: white;
  border-radius: 5px;
}
.removeBtn {
  margin-left: auto;
  color: #de4343;
}
.checkBtn {
  line-height: 45px;
  color: #62acde;
  margin-right: 5px;
}
.checkBtnCompleted {
  color: #b3adad;
}
.textCompleted {
  text-decoration: line-through;
  color: #b3adad;
}
</style>
