<template>
  <div id="input-container">
    <input
      type="text"
      id="name"
      v-model="name"
      placeholder="Enter name..."
    /><br />
    <input
      type="text"
      id="email"
      placeholder="Enter email..."
      v-model="email"
    /><br />
    <button v-on:click="addNew">Add</button>
  </div>
</template>

<script>
export default {
  name: 'CreateUser',
  data() {
    return {
      name: '',
      email: ''
    };
  },
  methods: {
    addNew: function() {
      const newPerson = {
        name: this.name,
        email: this.email
      };
      this.$emit('add-person', newPerson);
      (this.name = ''), (this.email = '');
    }
  }
};
</script>

<style scoped>
input,
button {
  margin: 0.3rem;
  padding: 0.2rem;
  width: 100%;
}
button {
  width: 100px;
}

#input-container {
  max-width: 400px;
  margin: auto;
  margin-bottom: 3rem;
}
</style>
