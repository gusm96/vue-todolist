<template>
  <main>
    <div>
      <ul>
        <li v-for="{ todoItem, index } in todoItems" v-bind:key="todoItem">
          {{ todoItem }}
          <button v-on:click="removeTodo(todoItem, index)">Delete</button>
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
          this.todoItems.push(localStorage.key(i));
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
      if (yesNo == true) {
        localStorage.removeItem(todoItem);
        this.todoItems.splice(index, 1);
      }
    }
  }
};
</script>
<style scoped></style>
