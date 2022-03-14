<template>
  <div id="app">
    <h1>Q&#38;A Buddy</h1>
    <label for="username">Username (first name + last name, all lowercase and no spaces. E.g. John Smith would be johnsmith)</label><br><br>
    <input type="text" id="username" name="username" v-model="username">
    <input type="submit" value="Submit" v-on:click="showPlanning">

    <Planning v-if="show_planning" v-bind:username="username"/>
    <Daily v-if="show_daily" v-bind:username="username"/>
    <Blocker v-if="show_blocker" v-bind:username="username"/>
  </div>
</template>

<script>

import Planning from '@/components/Planning.vue'
import Daily from '@/components/Daily.vue'
import Blocker from '@/components/Blocker.vue'
import $ from 'jquery'
export default {
  name: 'App',
  components: {
    Planning,
    Daily,
    Blocker,
  },

    watch: {
    show_planning() {
      console.log("show_planning changed")
    }
  },

  data () {
    return {
      username: null,
      show_planning: null,
      show_daily: null,
      show_blocker: null,
    }
  },
  methods: {
    
    showPlanning () {
      this.$data.show_daily = true
      this.$data.show_blocker = true
      if (this.$data.show_planning == false){
        // pass
      }
      else {
          this.$data.show_planning = true
      }

      if (this.$data.show_daily){
        // pass
      }


      
    }
    
  },

  created(){
    $.getJSON('https://sunrisesapp.com/qabuddy/get_unplanned.php?username='+this.$props.username, function (data) {
        console.log(data);
        
        if (data[0]['lecture'][0] != "n" && data[0]['course_material'][0] != "n" && data[0]['read_assignment'][0] != "n" && data[0]['part_one'][0] != "n" && data[0]['part_two'][0] != "n"
        && data[0]['part_three'][0] != "n" && data[0]['debug'][0] != "n" && data[0]['submit'][0] != "n"){
            self.$data.show_planning = false
        }

      });
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
