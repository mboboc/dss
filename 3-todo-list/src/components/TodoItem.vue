<template>
  <div class="todo-box">
    <span v-if="editable">
      <input v-model="description" />
      <button
        v-on:click="
          viewMode();
          editItem(id, description);
        "
      >
        Save
      </button>
    </span>
    <span v-else>
      <p>{{ description }}</p>
      <button v-on:click="deleteItem(id)">Delete</button>
      <button v-on:click="editMode">Edit</button>
    </span>
  </div>
</template>

<script>
export default {
  name: "TodoItem",
  props: {
    description: String,
    id: Number,
  },
  data() {
    const editable = false;
    return {
      editable,
    };
  },
  methods: {
    editMode: function () {
      this.editable = true;
    },
    viewMode: function () {
      this.editable = false;
    },
    deleteItem: function (id) {
      this.$emit("delete", id);
    },
    editItem: function (id, description) {
      this.$emit("edit", id, description);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.todo-box {
  width: 320px;
  padding: 10px;
  border: 5px solid gray;
  margin: 0;
}
</style>
