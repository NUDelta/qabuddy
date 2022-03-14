<template>
  <div class="main">
      <br>
      <p>Ignore if you've already done this today</p>
      <form class="planning_form" @submit.prevent="getFormValues">
      <div v-for="u in undone" v-bind:key="u">
         <label><b>Have you finished {{u.replace(/_/g, " ") + " "}} </b></label><br><br>
         <label>Yes</label><input type="radio" value="Yes" v-bind:id="u" v-bind:name="u" checked><br><br>
          <label>No, because I'm stuck</label><input type="radio" value="No, because I'm stuck" v-bind:id="u" v-bind:name="u"><br><br> <!-- redirect to blocked -->
          <label>No, because I ran out of time</label><input type="radio" value="No, because I ran out of time" v-bind:id="u" v-bind:name="u"><br><br>
    </div>
    

    <input type="submit" value="Submit">
    </form>
  </div>
</template>

<script>

import $ from 'jquery'
export default {
  name: 'Daily',
  props: {
      username: null,
  },

  data () {
    return {
        undone: ["lecture", "course_material", "read_assignment", "part_one", "part_two", "part_three", "debug", "submit"],
    }
  },

  methods: {
      getFormValues: function () {
          
        var test = $('.planning_form').serialize()
        
        console.log(test)

        $.getJSON('https://sunrisesapp.com/qabuddy/update_daily.php?username=' + this.$props.username + '&' + test, function () { // "no" in this means that it's done

// ignore            
        })

        $( ".planning_form" ).css( "display", "none" );
         $( "p" ).css( "display", "none" );
        //console.log(test[0]['name'] + test[0]['value'])
        
    }
      
  },

  created(){

  
      
    
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

.planning_form{
    text-align: left;
    padding-left: 40%;
}
</style>
