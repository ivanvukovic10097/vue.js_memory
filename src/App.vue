import router from "./router";

<template>
  <div id="app">
    <router-view></router-view>
  </div>
</template>

<script>
export default {
  name: "app",
  components: {
    methods: {
    }
  }
};
</script>

<style>
body {
  background-color: #ebeff2;
}
#numberofcards {
  margin: 250px auto;
  width: 700px;
  text-align: center;
  font-family: "Avenir", Helvetica, Arial, sans-serif;
}
h1 {
  margin: 0 auto;
  margin-bottom: 20px;
  font-size: 48px;
  font-weight: 300;
}
h3 {
  font-size: 15px;
  font-weight: 20px;
  color: #CC2039;
}
ul {
  margin: 0;
  padding: 0;
  list-style: none;
}
li {
  margin: 0;
  padding: 0;
  margin-bottom: 40px;
}
li > * {
  text-align: center;
  display: block;
  margin: 0 auto;
  width: 160px;
  padding: 30px;
  text-decoration: none;
  background-color: #CC2039;
  color: white;
  border-radius: 4px;
  box-shadow: 1px 1px 3px rgba(0, 0, 0, 0.12), 0 1px 2px rgba(0, 0, 0, 0.24);
  font-size: 25px;
  font-weight: 900;
  font-style: bold;
  transition: 0.4s ease;
}
li > *:hover {
  box-shadow: 0 14px 28px rgba(0, 0, 0, 0.25), 0 10px 10px rgba(0, 0, 0, 0.22);
  background-color: #c9102a;
  color: #ebeff2;
  width: 175px;
}
</style>
