<template>
  <h2>{{convoName}}</h2>
  <button type="button">Restart</button>

  <audio controls src="http://www.stillbrook.org/audio/office_ambience.mp3" />
  <div v-for="convoline in lines">
    <Line v-bind:line="convoline" v-if="convoline.visible" @selectLine="onNextLine" />
  </div>
</template>

<script>
import axios from 'axios'; 
import Line from './Line.vue'

export default {
  name: 'Conversation',
  components: {
    Line
  },
  props: {
    convo: String,
    difficulty: Number,
  },
  data() {
    return {
      info : 'another thing',
      convoName : 'My Dinner with Andre',
      lines : [
        {
          visible : true,
          next : 1,
          prev : null,
          speaker : 1,
          selected : '',
          options : {
            abc : { 
              text : "This is one",
              translation : 'This is one'
            },
            def : { 
              text : "this is another",
              translation : 'This is another'
            }
          }
        },
        {
          visible : false,
          next : 2,
          prev : 0,
          speaker : 2,
          selected : '',
          options : {
            ghi : { 
              text : "Banana",
              translation : 'Banana'
            },
            jkl : { 
              text : "Yellow",
              translation : "Yellow"
            }
          }
        },
        {
          visible : false,
          next : null,
          prev : 1,
          speaker : 1,
          selected : '',
          options : {
            mno : { 
              text : "My name is Sam", 
              translation : 'My name is Sam'
            },
            pqr : { 
              text : "My name is Jocelyn",
              translation : 'My nam is Jocelyn'
            }
          }
        },

      ]
    }
  },
  methods : {
    onNextLine(nextLineIndex) {
      if (nextLineIndex) {
        this.lines[nextLineIndex].visible = true;
      }
    }
  },
  mounted () {
    axios
      .get('https://api.coindesk.com/v1/bpi/currentprice.json')
      .then(response => (this.info = response.data.bpi["GBP"]))
  }
}
</script>

<style scoped>
</style>