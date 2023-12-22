<script>
export default {
  data: function () {
    return {
      todoItems: []
    }
  },
  created() {
    if (localStorage.length > 0) {
      for (var i = 0; i < localStorage.length; i++) {
        if(localStorage.key(i) !== 'loglevel:webpack-dev-server') {
          this.todoItems.push(JSON.parse(localStorage.getItem(localStorage.key(i))));
        }
      }
    }
  },
  // props속성 추가
  props: ['propsdata'],
  methods: {
    removeTodo(todoItem, index) {
      this.$emit('removeTodo', todoItem, index);
    }
  }
}
</script>
<template>
  <section>
    <transition-group name="list" tag="ul">
      <li v-for="(todoItem, index) in propsdata" v-bind:key="todoItem" class="shadow">
        <span class="checkBtn" v-bind:class="{checkBtnCompleted: todoItem.completed}" v-on:click="toggleComplete(todoItem)">
          <font-awesome-icon :icon="['fasr', 'check']" />
        </span>
        <span v-bind:class="{textCompleted: todoItem.completed}" v-on:click="toggleComplete(todoItem, index)">
          {{ todoItem }}
        </span>
        <span class="removeBtn" type="button" v-on:click="removeTodo(todoItem, index)">
          <font-awesome-icon :icon="['far', 'fa-trash-alt']" aria-hidden="true"/>
        </span>
      </li>
    </transition-group>
  </section>
</template>

<style scoped>
ul {
  list-style-type: none;
  padding-left: 0;
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
.checkBtn{
  color: cornflowerblue;
  padding-right: 6px;
}

</style>