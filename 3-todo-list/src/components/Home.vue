<template>
  <div>
    <ul>
      <li v-for="item in todoList" :key="item.id">
        <TodoItem
            :description="item.description"
            v-on:delete-item="deleteItem"
            v-on:edit-item="editItem"
        />
        <br>
      </li>
      <h5>Add new todo item</h5>
      <input v-model="newitem" placeholder="Add description">
      <button v-on:click="addToList">Save</button>
    </ul>
  </div>
</template>

<script>
import TodoItem from "./TodoItem.vue";
export default {
  name: "Home",
  components: {
    TodoItem,
  },
  data() {
    const todoList = [
      { id: 0, description: "Get A" },
      { id: 1, description: "Get B" },
      { id: 2, description: "Get C" },
    ];
    const newitem = "";
    return {
        todoList,
        newitem,
    }
  },
  methods: {
    addToList: function () {
        this.todoList.push({ id: this.todoList.length, description: this.newitem })
    },
    deleteItem: function () {
        console.log("Delete")
    },
    editItem: function () {
        console.log("Edit")
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
