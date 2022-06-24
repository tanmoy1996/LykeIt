<template>
  <v-card height="100%" :dark="dark" flat class="transparent d-flex align-center" >
    <div class="d-flex pa-15 no-outline" @keypress="key($event)" tabindex="0">
      <span class="mr-1">{{no}}.</span>
      <div >
        <p class="text-work-san f-24"> {{question}} 
          <span v-if="required">*</span>
        </p>
        <p class="text-work-san f-20 opacity-50"> {{questionDesc}} </p>
        <div id="range" v-if="parseInt(range)>0 && parseInt(range)<=15"
          class="d-flex flex-wrap ">
          <div v-for="i of parseInt(range)"
          :key="i"
          class="range pa-0 ma-3"
          :class="selected==i?'rangeSelected blink':null"
          @click="selectAns(i)">
            <p class="text-work-san f-16 mb-0">{{i}}</p>
          </div>
        </div>
        <div v-else
        class="pt-8">
          <v-slider
          v-model="selected"
          :dark="dark"
          track-color="grey"
          thumb-label="always"
          :color="dark?'white':'black'"
          :max="parseInt(range)"
          :class="dark?'li-slider':null"
          :thumb-color="dark?'white':'grey darken-3'"
          @change="updateValue($event)"/>
        </div>
        <v-btn :light="dark" :dark="!dark" class="mt-3">
          OK
          <v-icon right>mdi-check</v-icon>
        </v-btn>
      </div>
    </div>
  </v-card>
</template>

<script>
export default {
  name:"Range",
  props:{
    value:String,
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
  data(){
    return{
      selected:0,
      
    }
  },
  methods:{
    selectAns(idx){
      if(this.selected==idx){
        this.selected=-1;
      }
      else{
        this.selected=idx;
      }
      this.updateValue(`${this.selected}`);
    },
    key(e) {
      if(e.keyCode>48 && e.keyCode<59){
        this.selectAns(e.key);
      }
    },
    updateValue(value){
      this.$emit('input',`${value}`);
    }
  }
}
</script>

<style>
  .li-slider .v-slider__thumb-label>div>span{
    color:black;
    font-family: 'Work Sans', sans-serif;
  }
</style>
<style scoped>
.answer{
  font-size:28px;
}
.answer .v-select__slot{
  padding: 10px 0;
}
.option{
  border: 2px solid white;
  border-radius: 5px;
  position: relative;
  min-height:50px;
  min-width: 15vw;
  transition: all 100ms ease-in-out;
}
.option img{
  max-width:200px;
}
.range{
  border: 1px solid white;
  border-radius: 5px;
  width:70px;
  height:70px;
  display: flex;
  align-items: center;
  justify-content: center;
}
.range:hover{
  background: rgba(255, 255, 255, 0.25);
}
.rangeSelected{
  background: rgb(255, 255, 255);
  color:black;
}
.range>p{
  font-size: 28px;
}
.selected{
  top:-1px;
  right:-1px;
  height:48px;
  width: 48px;
  border-radius: 5px;
  position: absolute;
  background: white;
  clip-path: polygon(0% 0, 100% 0, 100% 100%);
}
.f-16{
  font-size: 16px;
}
.blink {
  animation: blinker 500ms linear 2;
}
.keyboard{
  background: rgba(255, 255, 255, 0.747) !important;
  color:rgb(24, 24, 24);
  transition: all 100ms ease-in-out;
}
.option:hover{
  background: rgba(255, 255, 255, 0.205);
}
.option:hover .keyboard{
  background: rgba(255, 255, 255) !important;
  color:rgb(2, 2, 2);
}
@keyframes blinker {
  0% {
    border: 2px solid white;
  }
  33% {
    border: 2px solid rgb(54, 54, 54);
  }
  66% {
    border: 2px solid white;
  }
}

</style>