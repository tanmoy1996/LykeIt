<template>
  <v-card height="100%" :dark="dark" flat class="transparent d-flex align-center" >
    <div class="d-flex pa-md-15 pa-5 no-outline" @keypress="key($event)" tabindex="0">
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
          class="range pa-0 ma-md-3 mr-1 mb-1"
          :class="`range${dark?'Dark':'Light'} ${selected==i?dark?'blink dark':'blink light':''} `"
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
        <v-btn :light="dark" :dark="!dark" class="mt-3" @click="$emit('next');">
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
      setTimeout(()=>{this.$emit('next')}, 1000);
      
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
.range{
  border-radius: 5px;
  width:70px;
  height:70px;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
}
.rangeLight{
  border: 2px solid rgb(65, 65, 65);
}
.rangeDark{
  border: 2px solid white;

}
.dark{
  background: white;
  color:rgb(65, 65, 65);
}
.light{
  background: rgb(51, 51, 51);
  color:white;
}

.range>p{
  font-size: 28px;
}
.f-16{
  font-size: 16px;
}
.blink {
  animation: blinker 500ms linear 2;
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
@media (max-width: 480px) {
  .option{
  min-width: 50vw;
  }
  .range{
    width:50px;
    height:50px;
  }
}
</style>