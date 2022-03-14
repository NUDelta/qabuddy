<template>
  <div class="main">
      <br>
      <form class="planning_form" @submit.prevent="getFormValues">
      <div v-for="u in undone" v-bind:key="u">
         <label>When will you do {{u.replace(/_/g, " ") + " "}} (leave blank if not doing it) </label>
         <input type="datetime-local" value="2021-01-27T08:30" v-bind:id="u" v-bind:name="u"><br><br>
    </div>
    

    <input type="submit" value="Submit">
    </form>
  </div>
</template>

<script>

import $ from 'jquery'
export default {
  name: 'Planning',
  props: {
      username: null,
  },

  data () {
    return {
        undone: [],
    }
  },

  methods: {
      getFormValues: function () {
          
        var test = $('.planning_form').serialize()
        
        console.log(test)

        $.getJSON('https://sunrisesapp.com/qabuddy/update_user_planning.php?username=' + this.$props.username + '&' + test, function () { // "no" in this means that it's done

// ignore            
        })
        //console.log(test[0]['name'] + test[0]['value'])
        
    }
      
  },

  created(){

  
      var self = this;
        console.log("in created");
      $.getJSON('https://sunrisesapp.com/qabuddy/get_unplanned.php?username='+this.$props.username, function (data) {
        console.log(data);
        
        if (data[0]['lecture'][0] == "n"){
            self.undone.push("lecture")
        }
        if (data[0]['course_material'][0] == "n"){
            self.undone.push("course_material")
        }
        if (data[0]['read_assignment'][0] == "n"){
            self.undone.push("read_assignment")
        }
        if (data[0]['part_one'][0] == "n"){
            self.undone.push("part_one")
        }
        if (data[0]['part_two'][0] == "n"){
            self.undone.push("part_two")
        }
        if (data[0]['part_three'][0] == "n"){
            self.undone.push("part_three")
        }
        if (data[0]['debug'][0] == "n"){
            self.undone.push("debug")
        }
        if (data[0]['submit'][0] == "n"){
            self.undone.push("submit")
        }


        
      });
      
    
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
