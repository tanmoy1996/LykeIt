<template>
  <v-card height="100%" :dark="dark" flat class="transparent d-flex align-center">
    <div class="d-flex pa-15">
      <span class="mr-1">{{no}}.</span>
      <div>
        <p class="text-work-san f-24"> {{question}} 
          <span v-if="required">*</span>
        </p>
        <p class="text-work-san f-20 opacity-50"> {{questionDesc}} </p>
        <div v-if="bool">
          <v-col v-for="(option,idx) of opt"
          cols="5"
          :key="idx"
          class="option pa-0 ma-3"
          :class="selected==idx?'blink':null"
          @click="selectAns(idx)">
            <v-card outlined class="transparent">
              <!-- keyboard option -->
              <div class="d-flex ma-2 mt-3">
                <v-card flat class="transparent px-2 mr-2 rounded-sm keyboard">
                  <b class="text-work-san f-16">{{option.charAt(0)}}</b>
                </v-card>
                <p class="text-work-san f-16 mb-0">{{option}}</p>
              </div>
            </v-card>
            <div v-if="selected==idx" class="d-flex align-start justify-end selected">
              <v-icon color="black">mdi-check</v-icon>
            </div>
          </v-col>
        </div>
        <div v-else-if="parseInt(range)>0 && parseInt(range)<=36"
          class="d-flex flex-wrap ">
          <div v-for="i of parseInt(range)"
          :key="i"
          class="range pa-0 ma-3"
          :class="selected==i?'rangeSelected blink':null"
          @click="selectAns(i)">
            <p class="text-work-san f-16 mb-0">{{i}}</p>
          </div>
        </div>
        <div v-else-if="parseInt(range)>0 && parseInt(range)>36"
          class="d-flex flex-wrap ">
          <p class="text-work-san f-16 mb-0">
            The range should be less than 36
          </p>
        </div>
        <div v-else-if="options.length==2" 
        class="space-around"
        :class="options[0].pic?'d-flex':null">
          <v-col cols="5" v-for="(option,idx) of options" 
          :key="idx" 
          class="option pa-0 ma-3"
          :class="selected==idx?'blink':null"
          @click="selectAns(idx)">
            <v-card outlined class="transparent">
              <div class="d-flex align-center justify-center">
                <img :src="option.pic" width="50%"/>
              </div>
              <!-- keyboard option -->
              <div class="d-flex ma-2">
                <v-card flat class="white black--text px-2 mr-2 rounded-sm">
                  <b class="text-work-san f-16">{{String.fromCharCode(65+idx)}}</b>
                </v-card>
                <p class="text-work-san f-16 mb-0" v-text="option.name"></p>
              </div>
            </v-card>
            <div v-if="selected==idx" class="d-flex align-start justify-end selected">
              <v-icon color="black">mdi-check</v-icon>
            </div>
          </v-col>
        </div>
        <div v-else-if="options.length>2 && options.length<=6" 
        class="d-flex flex-wrap space-around">
          <div v-for="(option,idx) of options" 
          :key="idx" 
          class="option pa-0 ma-3"
          :class="selected==idx?'blink':null"
          @click="selectAns(idx)">
            <v-card outlined class="transparent">
              <div class="d-flex align-center justify-center">
                <img :src="option.pic" width="50%"/>
              </div>
              <!-- keyboard option -->
              <div class="d-flex ma-2">
                <v-card flat class="white black--text px-2 mr-2 rounded-sm">
                  <b class="text-work-san f-16">{{String.fromCharCode(65+idx)}}</b>
                </v-card>
                <p class="text-work-san f-16 mb-0" v-text="option.name"></p>
              </div>
            </v-card>
            <div v-if="selected==idx" class="d-flex align-start justify-end selected">
              <v-icon color="black">mdi-check</v-icon>
            </div>
          </div>
        </div>
        <div v-else-if="options.length>6">
          <v-autocomplete
            :items="options"
            item-text="name"
            placeholder="Type or select an option"
            class="text-work-san answer"
            :multiple="multiple"
          ></v-autocomplete>
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
  name:"Mcq",
  props:{
    no: String,
    range: String,
    question: String,
    questionDesc: String,
    options: {
      type: Array,
      default(){
        return [];
      },
    },
    bool: {
      type: Boolean,
      default: false,
    },
    dark: {
      type: Boolean,
      default: false,
    },
    required: {
      type: Boolean,
      default: false
    },
    multiple: {
      type: Boolean,
      default: false
    }
  },
  data(){
    return{
      selected:-1,
      opt:['True','False'],
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
    }
  }
}
</script>

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