<template>
  <main>
    <div class="inputBox shadow">
      <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo" />
      <span class="addContainer" v-on:click="addTodo">
        <i class="fa-solid fa-plus addBtn"></i>
      </span>
      <Modal v-if="showModal" @close="showModal = false">
        <h3 slot="header">
          경고!
        </h3>
      </Modal>
    </div>
  </main>
</template>
<script>
import Modal from "./common/Modal.vue";
export default {
  name: "TodoInput",
  data() {
    return {
      newTodoItem: "",
      showModal: false
    };
  },
  methods: {
    addTodo: function() {
      if (this.newTodoItem !== "") {
        // $emit을 이용하여 상위 컴포넌트인 App.vue 로 addTodoItem를 보내준다.
        this.$emit("addTodoItem", this.newTodoItem);
        this.clearInput();
      } else {
        this.showModal = !this.showModal;
      }
    },
    clearInput: function() {
      this.newTodoItem = "";
    }
  },
  components: {
    Modal: Modal
  }
};
</script>
<style scoped>
input:focus {
  outline: none;
}
.inputBox {
  background-color: white;
  height: 50px;
  line-height: 50px;
  border-radius: 5px;
}
.inputBox input {
  border-style: none;
  font-size: 0.9rem;
}
.addContainer {
  float: right;
  background: linear-gradient(to right, #6478fb, #8763fb);
  display: block;
  width: 3rem;
  border-radius: 0 5px 5px 0;
  cursor: pointer;
}
.addBtn {
  color: white;
  vertical-align: middle;
}
</style>
