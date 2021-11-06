<!-- XXX
  The table is not reactive and the page needs to be refreshed for the changes to take action
  This is most likely because localStorage is not reactive
 -->

<template>
  <div>
    <ul>
      <li v-for="item in todoList" :key="Object.keys(item)">
        <TodoItem
          :description="Object.values(item)[0]"
          :id="Object.keys(item)[0]"
          v-on:delete="deleteItem"
          v-on:edit="editItem"
        />
      </li>
      <h5>Add new todo item</h5>
      <input v-model="newitem" placeholder="Add description" />
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
    const newitem = "";
    return {
      newitem,
    };
  },
  computed: {
    todoList() {
      var values = [],
        keys = Object.keys(localStorage),
        i = keys.length;

      while (i--) {
        if (localStorage.getItem(keys[i]) != "SILENT") {
          var key = keys[i];
          values.push({ [key]: localStorage.getItem(key) });
        }
      }

      console.log(values);
      return values;
    },
  },
  methods: {
    addToList: function () {
      window.localStorage.setItem(Date.now(), this.newitem);
    },
    deleteItem: function (id) {
      console.log("Delete " + id);
      window.localStorage.removeItem(id);
    },
    editItem: function (id, description) {
      console.log("Edit " + id + " " + "<" + description + ">");
      window.localStorage.setItem(id, description);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
