<template>
  <h2>{{convoName}}</h2>

  <audio controls />
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
    convo: String
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
              translation : {
                en : 'This is one'
              } 
            },
            def : { 
              text : "this is another",
              translation : {
                e : 'This is another'
              }
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
              translation : {
                en : 'Banana'
              }
            },
            jkl : { 
              text : "Yellow",
              translation : {
                en : "Yellow"
              }
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
              translation : {
                en : 'My name is Sam'
              } 
            },
            pqr : { 
              text : "My name is Jocelyn",
              translation : {
                en : 'My nam is Jocelyn'
              } 
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