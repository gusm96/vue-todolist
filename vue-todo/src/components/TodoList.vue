<template>
  <main>
    <div>
      <ul>
        <li v-for="(todoItem, index) in propsdata" v-bind:key="todoItem.item">
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
  props: ["propsdata"],
  methods: {
    removeTodo: function(todoItem, index) {
      this.$emit("removeItem", todoItem, index);
    },
    toggleComplete: function(todoItem, index) {
      this.$emit("toggleItem", todoItem, index);
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
