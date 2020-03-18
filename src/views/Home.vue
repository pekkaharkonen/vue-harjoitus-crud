<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png" />
    <CreateUser v-on:add-person="addPerson" />
    <UsersList
      v-bind:users="users"
      v-on:delete-user="deleteUser"
      v-on:edit-user="editUser"
    />
  </div>
</template>

<script>
// @ is an alias to /src
import Axios from 'axios';
import UsersList from '../components/UsersList';
import CreateUser from '../components/CreateUser';

export default {
  name: 'Home',
  components: {
    UsersList,
    CreateUser
  },
  data() {
    return {
      users: []
    };
  },
  created() {
    this.fetchData();
  },
  methods: {
    async fetchData() {
      let response = await Axios.get('http://localhost:3000/api/users');
      this.users = response.data;
    },
    async addPerson(newPerson) {
      await Axios.post('http://localhost:3000/api/users', newPerson);
      this.fetchData();
    },
    async deleteUser(id) {
      await Axios.delete(`http://localhost:3000/api/users/${id}`);
      this.fetchData();
    },
    async editUser(newUser) {
      await Axios.put(`http://localhost:3000/api/users/${newUser.id}`, newUser);
      this.fetchData();
    }
  }
};
</script>
