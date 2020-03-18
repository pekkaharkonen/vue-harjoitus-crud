<template>
  <div>
    UsersList
    <ul>
      <li v-for="user in users" :key="user.id">
        <User
          v-bind:user="user"
          v-on:delete-user="$emit('delete-user', user.id)"
          v-on:edit-user="handleEmit"
        />
      </li>
    </ul>
  </div>
</template>

<script>
import User from './User';
export default {
  name: 'UserList',
  props: {
    users: Array
  },
  components: {
    User
  },
  methods: {
    handleEmit: function(data) {
      this.$emit('edit-user', data);
    }
  }
};
</script>

<style scoped>
li {
  list-style: none;
}
</style>
