<template>
  <div class="home">

    <h1>{{ message }}</h1>

    <ul>
      <li v-for="error in errors"> {{ error }} </li>
    </ul>

    <div> <h4>Number of People: {{ people.length }} </h4></div>

    <div v-for="person in people">
      <h2 v-on:click="toggleBio(person)">Name: {{person.name}} </h2>
      <div v-if="person.bioVisible">
      <p>Bio: {{ person.bio }} </p>
      <button v-on:click="deletePerson(person)">Delete</button>
      </div>
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
.strike {
  text-decoration: line-through;
}
</style>

<script>

  var axios = require("axios");

export default {
  data: function() {
    return {
      message: "Intersting People",
      people: [],

      newPerson: {name: "", bio: "", bioVisible: true},

      errors: []
    };
  },
  created: function() {
    axios.get("http://localhost:3000/api/people").then(function(response) {
      this.people = response.data;
    }.bind(this));

  },
  methods: {
    addPerson: function() {
      this.errors = [];
      var params = {
                    name: this.newPerson.name,
                    bio: this.newPerson.bio
                   };
        
        axios
        .post("http://localhost:3000/api/people", params)



        .then(response => {
             this.people.push(response.data);
             this.newPerson = {name: "", bio: "", bioVisible: false};
          })


        .catch(error => {
          this.errors = error.response.data.errors;
        });
        

    },
    
    toggleBio: function(inputPerson) {
        inputPerson.bioVisible = !inputPerson.bioVisible;
    },
    deletePerson: function() {
      var index = this.people.indexOf(inputPerson);
      this.people.splice(index, 1);
    }
  },
  computed: {}
};
</script>