<template>
  <div class="main">
      <br>
      <p><b>Stuck?</b></p>
      
      <form class="blocker_form" @submit.prevent="getFormValues">

          <label>What are you stuck on</label><br><br>
         <input type="textarea" value=" " v-bind="stuck_on"><br><br>

         <label>What have you tried</label><br><br>
         <input type="textarea" value=" " v-bind="tried"><br><br>

         <label>What do you think your solution might be</label><br><br>
         <input type="textarea" value=" " v-bind="potential_solution"><br><br>

         <label>Based on your answers to the above questions, formulate a specific question you could ask on Campuswire or at Office Hours</label><br><br>
         <input type="textarea" value=" " v-bind="question"><br><br>


    

    <input type="submit" value="Submit">
    </form>
  </div>
</template>

<script>

import $ from 'jquery'
export default {
  name: 'Blocker',
  props: {
      username: null,
  },

  data () {
    return {
        stuck_on: null,
        tried: null,
        potential_solution: null,
        question: null,
        }
  },

  methods: {
      getFormValues: function () {
          
        var test = $('.planning_form').serialize()
        
        console.log(test)

        $.getJSON('https://sunrisesapp.com/qabuddy/user_stuck.php?username=' + this.$props.username + '&stuck_on=' + this.$data.stuck_on + '&tried=' + this.$data.tried + '&potential_solution=' + this.$data.potential_solution + '&question=' + this.$data.question, function () { // "no" in this means that it's done

// ignore            
        })

        alert("Thanks for filling it out!");
        $( ".blocker_form" ).css( "display", "none" );
        //console.log(test[0]['name'] + test[0]['value'])
        
    }
      
  },


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
input {
    width: 40vw;
    min-height: 20vh;
}
</style>
