<template>
  <footer>
    <div class="clearAllContainer">
      <span class="clearAllBtn" @click="clearTodo">
        Clear All
      </span>
    </div>
  </footer>
</template>
<script>
export default {
  name: "TodoFooter",
  components: {},
  data() {
    return {
      example: ""
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
    clearTodo: function() {
      const yesNo = confirm("정말로 모두 삭제하시겠습니까?");
      if (yesNo) {
        localStorage.clear();
        location.reload();
      }
    }
  }
};
</script>
<style scoped>
.clearAllContainer {
  width: 8.5rem;
  height: 50px;
  line-height: 50px;
  background-color: white;
  border-radius: 5px;
  margin: 0 auto;
  cursor: pointer;
}
.clearAllBtn {
  color: #e30303;
  /* 추가 */
  display: block;
}
</style>
