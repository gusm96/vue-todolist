<template>
  <main>
    <div>
      <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo" />
      <button v-on:click="addTodo">Submit</button>
    </div>
  </main>
</template>
<script>
export default {
  name: "TodoInput",
  components: {},
  data() {
    return {
      newTodoItem: ""
    };
  },
  beforeCreate() {},
  created() {},
  beforeMount() {},
  mounted() {},
  beforeUpdate() {},
  updated() {},
  beforeUnmount() {},
  unmounted() {},
  methods: {
    addTodo: function() {
      localStorage.setItem(this.newTodoItem, this.newTodoItem);
      this.clearInput();
    },
    clearInput: function() {
      this.newTodoItem = "";
    }
  }
};
</script>
<style scoped></style>
