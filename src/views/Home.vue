<template>
  <div class="home">

    <h1>{{ message }}</h1>

    <div> <h4>Number of People: {{ count }} </h4></div>

    <div v-for="person in people">
      <h2>Name: {{person.name}} </h2>
      <p>Bio: {{ person.bio }} </p>
    </div>

    

    <div>
      <h4>Create New Person</h4>
      Name: <input v-model="newPerson.name">
      Bio: <input v-model="newPerson.bio">
      <button v-on:click="addPerson()">Add Person</button>
    </div>
  </div>
</template>

<style>
</style>

<script>
export default {
  data: function() {
    return {
      message: "People",
      people: [
      {name: "Martha Vineyard", bio: "An elegant lady that likes expensive things and wine.", bioVisible: true},
      {name: "Yeller Longfoot", bio: "From deep south, likes chewing tobacco and his hound dog.", bioVisible: true}],

      newPerson: {name: "", bio: "", bioVisible: true},
    };
  },
  created: function() {},
  methods: {
    addPerson: function() {
      this.people.push(this.newPerson);
      this.newPerson = {name: "", bio: "", bioVisible: true};
    },
    countPeople: function() {
      var count = this.people.length;
    }
  },
  computed: {}
};
</script>