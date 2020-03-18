<template>
  <div>
    <div id="item">
      <span>{{ user.name }}, {{ user.email }}</span>
      <span id="buttons"
        ><button v-on:click="editUser">Edit</button
        ><button v-on:click="$emit('delete-user', user.id)">X</button></span
      >
    </div>
    <div v-if="showEdit" id="edit-component">
      <input
        type="text"
        id="name"
        placeholder="Enter new name"
        v-model="editName"
      /><br />
      <input
        type="text"
        id="email"
        placeholder="Enter new email"
        v-model="editEmail"
      /><br />
      <button v-on:click="handleEdit">Confirm edit</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'User',
  props: {
    user: Object
  },
  data() {
    return {
      showEdit: false,
      editName: '',
      editEmail: ''
    };
  },
  methods: {
    editUser: function() {
      this.showEdit = !this.showEdit;
    },
    handleEdit: function() {
      const newUser = {
        name: this.editName,
        email: this.editEmail,
        id: this.user.id
      };
      this.$emit('edit-user', newUser);
    }
  },
  mounted() {
    this.editName = this.user.name;
    this.editEmail = this.user.email;
  }
};
</script>

<style scoped>
#item {
  display: flex;
  justify-content: space-between;
  max-width: 500px;
  margin: auto;
}

#edit-component {
  margin: 0.7rem 0;
}
</style>
