<template>
  <div class="todo-box">
      <span v-if="editable">
        <input v-model="description">
        <button v-on:click="viewMode">Save</button>
      </span>
      <span v-else>
        <p>{{ description }}</p>
        <button> Delete </button>
        <button v-on:click="editMode">Edit</button>
      </span>
  </div>
</template>

<script>
export default {
  name: 'TodoItem',
  props: {
    description: String
  },
  data () {
    const editable = true;
    return {
        editable,
    }
  },
  methods: {
    editMode: function () {
        this.editable = true
    },
    viewMode: function() {
        this.editable = false
    },
    deleteItem: function() {
        this.$emit('delete-item')
    },
    saveItem: function() {
        this.$emit('edit-item')
    }
  }
}
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
