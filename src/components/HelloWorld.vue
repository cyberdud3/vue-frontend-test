<template>
  <div class="hello">
    <h2>LOGIN</h2>
    <div style="margin: 10px">UserName: <input v-model="name" /></div>
    <div style="margin: 10px">Password: <input v-model="password" /></div>
    <button style="margin: 10px" @click="login">Login</button>
    <div style="margin: 10px; color: green; font-size: 24px">
      {{ repsonse }}
    </div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  data() {
    return {
      repsonse: "",
      name: "",
      password: "",
    };
  },
  methods: {
    login() {
      console.log(this.name, this.password, "check");
      fetch(`http://localhost:8080/login`, {
        method: "POST",
        body: JSON.stringify({ username: this.name, password: this.password }),
        headers: {
          "Content-Type": "application/json",
        },
      })
        .then((val) => val.json())
        .then((val) => {
          console.log(val, "Values send");
          this.repsonse = "Success";
        })
        .catch((val) => {
          console.log(val);
          this.repsonse = "Failed";
        });
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1,
h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
