<template>
  <div class="single-line">
    <div class="speak-button"><i class="fas fa-play"></i></div>
    <div v-bind:class="getLineClass()" @click="selectLine()">{{line.text}}</div>
    <button v-show="isTextBlurred" @click="unblurText()"><i class="fas fa-eye"></i></button>
  </div>
</template>

<script>
export default {
  name: 'SingleLine',
  props: {
      id : String,
      line: Object,
      speaker : Number,
      displayClearText : Boolean,
  },
  data() {
    return {
      key: "nothing",
      isTextBlurred : false
    }
  },
  mounted () {
    this.isTextBlurred = this.speaker == 2 && !this.displayClearText;
  },
  methods : {
    getLineClass() {
      const fuzz = this.isTextBlurred ? 'blurred' : '';
      return 'line-text ' + fuzz;
    },
    unblurText() {
      this.isTextBlurred = false;
    },
    selectLine() {
      this.$emit('line-selected', this.id);
    }
  }
}
</script>

<style scoped>
.blurred {
  filter: blur(4px);
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

.line-text {
  display: inline-block;
}
</style>