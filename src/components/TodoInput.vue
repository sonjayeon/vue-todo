<template>
  <div class="inputBox shadow">
    <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo">
    <span class="addContainer" v-on:click="addTodo">
      <font-awesome-icon :icon="['far', 'square-plus']" aria-hidden="true" style="color: white; vertical-align: middle" />
    </span>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTodoItem: ""
    }
  },
  props: ['propsdata'],
  methods: {
    addTodo() {
      if (this.newTodoItem !== '') {
        var value = this.newTodoItem && this.newTodoItem.trim();
        this.$emit('addTodo', value);
        // 지정하는 로직
        this.clearInput();
      }
    },
    clearInput() {
      this.newTodoItem = "";
    }
  }
}
</script>
<style scoped>
input:focus {
  outline: none;
}
.inputBox {
  background: white;
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
  background: linear-gradient(to right, #62EAC6, #32CEE6);
  display: block;
  width: 3rem;
  border-radius: 0 5px 5px 0;
}

</style>