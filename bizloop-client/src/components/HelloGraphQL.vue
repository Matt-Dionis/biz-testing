<template>
  <div id="app">
    <h1>{{ msg }}</h1>
    <h2>To Get Started Please SignUp Below:</h2>
    <input type="text" placeholder="First Name" v-model="fname">
    <input type="text" placeholder="Last Name" v-model="lname">
    <input type="text" placeholder="Email" v-model="email">
    <input type="password" placeholder="Password" v-model="password">
    <input type="password" placeholder="Confirm Password" v-model="password2">
    <button @click="signup()">Submit</button>

  </div>
</template>

<script>
import gql from "graphql-tag";

export default {
  name: "HelloGraphQL",
  data() {
    return {
      msg: "Welcome to BizLoop",
      feed: "", // Apollo will assign the result of its "feed" query here!
      fname: "",
      lname: "",
      email: "",
      password: ""
    };

    name = fname + lname;
  },
  apollo: {
    // Apollo specific options
    // Here, we use gql to describe the data we want: a feed with ID 1, and
    // Apollo will assign the result of that query to the 'feed' key in data.
    methods: {
      signup() {
        const { email, name, password } = this.$data;
        this.$apollo.mutate({

          mutation: gql 'mutation ($name: Name, $email: Email, $password: Password) {
            signup(name: $name, email: $email, password: $password) {
             id 
             }
             }'
        });
      }
    }
  }
};
</script>
