<template>
  <v-card height="100%" :dark="dark" flat class="transparent d-flex align-center" >
    <div class="d-flex pa-md-15 pa-5 no-outline" @keypress="key($event)" tabindex="0">
      <span class="mr-1">{{no}}.</span>
      <div >
        <p class="text-work-san f-24"> {{question}} 
          <span v-if="required">*</span>
        </p>
        <p class="text-work-san f-20 opacity-50"> {{questionDesc}} </p>
        <v-row id="range" v-if="parseInt(range)>0 && parseInt(range)<=10">
          <v-col v-for="i of parseInt(range)" :key="i" @click="selectAns(i)">
            <Button width="70" height="70"><b>{{i}}</b></Button>
          </v-col>
        </v-row>
        <div v-else
        class="pt-8">
          <v-slider
            v-model="selected"
            :dark="dark"
            track-color="grey"
            thumb-label="always"
            :color="dark?'white':'black'"
            :max="parseInt(range)"
            class="li-range"
            :class="dark?'li-slider':null"
            :thumb-color="dark?'white':'grey darken-3'"
            @change="updateValue($event)"/>
          <Button width="85" class="mt-4" @click="$emit('next');">
            <div class="d-flex">
              <p class="mb-0 grey--text text--darken-3 f-16">ok</p>
              <v-icon color="grey darken-3" class="ml-2">mdi-arrow-right-thin</v-icon>
            </div>
        </Button>
        </div>
      </div>
    </div>
  </v-card>
</template>

<script>
import Button from '../Button.vue';
export default {
    name: "Range",
    components: { Button },
    props: {
        value: String,
        no: String,
        question: String,
        questionDesc: String,
        range: String,
        dark: {
            type: Boolean,
            default: false,
        },
        required: {
            type: Boolean,
            default: false
        },
    },
    data() {
        return {
            selected: 0,
        };
    },
    methods: {
        selectAns(idx) {
            if (this.selected == idx) {
                this.selected = -1;
            }
            else {
                this.selected = idx;
            }
            this.updateValue(`${this.selected}`);
            setTimeout(() => { this.$emit("next"); },400);
        },
        key(e) {
            if (e.keyCode > 48 && e.keyCode < 59) {
                this.selectAns(e.key);
            }
        },
        updateValue(value) {
            this.$emit("input", `${value}`);
        }
    },
}
</script>

<style>
  .li-range .v-slider__track-fill{
    height:5px;
    border-radius: 3px;
  }
  .li-range .v-slider__track-background{
    height:5px;
    border-radius: 3px;
  }
</style>