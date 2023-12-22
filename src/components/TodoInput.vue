<template>
  <div class="inputBox shadow">
    <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo" placeholder="Type what you have to do">
    <span class="addContainer" v-on:click="addTodo">
      <font-awesome-icon :icon="['far', 'square-plus']" aria-hidden="true" style="color: white; vertical-align: middle" />
    </span>

    <alert-modal v-if="showModal" @close="showModal = false">
      <h3 slot="header">경고</h3>
      <span slot="footer" @click="showModal = false">할 일을 입력하세요.
        <font-awesome-icon :icon="['fasr', 'xmark']" aria-hidden="true"/>
      </span>
    </alert-modal>
  </div>
</template>

<script>


import AlertModal from "@/components/common/alertModal.vue";

export default {
  components: {AlertModal},
  data() {
    return {
      newTodoItem: "",
      showModal: false
    }
  },
  props: ['propsdata'],
  methods: {
    addTodo() {
      if (this.newTodoItem !== '') {
        var value = this.newTodoItem && this.newTodoItem.trim();
        this.$emit('addTodo', value);
        this.clearInput();
      } else {
        this.showModal = !this.showModal;
      }
    },
    clearInput() {
      this.newTodoItem = "";
    }
  },
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