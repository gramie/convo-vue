<template>
  <div>
    <div v-bind:class="getSpeaker()">
      <div class="line selected-line" v-if="line.selected">
          <SingleLine v-bind:line="line.options[line.selected]" v-bind:id="line.selected" v-bind:speaker="this.speaker" v-bind:displayClearText="false" />
      </div>
      <div v-else>
        <template v-for="(option, id) in line.options">
          <SingleLine v-bind:line="option" v-bind:id="id" v-bind:speaker="this.speaker" v-bind:displayClearText="false" v-on:line-selected="selectLine"/>
        </template>
      </div>
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
  mounted() {
    console.log("loaded");
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
</style>