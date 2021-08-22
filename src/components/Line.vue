<template>
  <SingleLine />
  <div v-bind:class="getSpeaker()">
    <div class="line selected-line" v-if="line.selected">
      <div class="speak-button"><i class="fas fa-play"></i></div>
      <span class="line-text" v-bind:title="line.options[line.selected].translation['en']">{{line.options[line.selected].text}}</span>
    </div>
    <div v-else>
      <template v-for="(option, id) in line.options">
        <div class="line available-line">
          <div class="speak-button"><i class="fas fa-play"></i></div>
          <div class="line-text" @click="selectLine(id)"> {{option.text}} </div>
        </div>
      </template>
    </div>
  </div>
</template>

<script>
import SingleLine from './SingleLine.vue';

export default {
  name: 'Line',
  components: {
    SingleLine,
  },
  props: {
      line: Object,      
  },
  data() {
    return {
      key: "nothing"
    }
  },
  mounted () {
  },
  methods : {
    getSelectedText() {
      if (this.line.selected) {
        return this.line.options[this.line.selected].text;
      } else {
        return 'nothing chosen';
      }
    },
    selectLine(id) {
      this.line.selected = id;
      this.$emit("selectLine", this.line.next);
    },
    getSpeaker() {
      return "speaker-" + this.line.speaker;
    }

  }
}
</script>

<style scoped>
.speaker-1 {
  text-align: left;
}
.speaker-2 {
  text-align: right;
}
.line {
  display: block;
}
.selected-line {
  border: 1px solid gray;
  background-color: #FEF;
  color: blue;
}
.line-text {
  display: inline-block;
}

.speak-button {
  border-radius: 50%;
  background-color: #04AA6D; /* Green */
  border: none;
  color: white;
  padding: 10px 10px 10px 12px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  margin: 2px 2px;
  cursor: pointer;
}

</style>