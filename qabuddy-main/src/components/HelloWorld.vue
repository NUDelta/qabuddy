<template>
  <div class="main">
    <label for="username">Username (first name + last name, all lowercase and no spaces. E.g. John Smith would be johnsmith)</label><br>
    <input type="text" id="username" name="username" v-model="username">
    <input type="submit" value="Submit">

  </div>
</template>

<script>
export default {
  name: 'HelloWorld',

  data () {
    return {
      username: null,
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
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
