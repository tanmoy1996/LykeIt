<template>
  <v-card height="100%" :dark="dark" flat class="transparent d-flex align-center">
    <div class="d-flex pa-15 no-outline" @keypress="key($event)" tabindex="0">
      <span class="mr-1">{{no}}.</span>
      <div>
        <p class="text-work-san f-24"> {{question}} 
          <span v-if="required">*</span>
        </p>
        <p class="text-work-san f-20 opacity-50"> {{questionDesc}} </p>
        <div>
          <div v-for="(option,idx) of opt"
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
          </div>
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
  name:"Bool",
  props:{
    value:Boolean,
    no: String,
    question: String,
    questionDesc: String,
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
      this.updateValue(this.selected==0)
    },
    key(e) {
      if(e.key.toLowerCase()=='t'){
      this.selectAns(0);
    }
    else if(e.key.toLowerCase()=='f'){
      this.selectAns(1);
    }
    },
    updateValue(value){
      this.$emit('input',value);
    },
  }
}
</script>

<style scoped>
.option{
  border: 2px solid white;
  border-radius: 5px;
  position: relative;
  min-height:50px;
  min-width: 15vw;
  max-width: 20vw;
  transition: all 100ms ease-in-out;
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