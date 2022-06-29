<template>
  <v-card height="100%" :dark="dark" flat class="transparent d-flex align-center">
    <div class="d-flex pa-md-15 pa-5 no-outline" @keypress="key($event)" tabindex="0">
      <span class="mr-1">{{no}}.</span>
      <div>
        <p class="text-work-san f-24"> {{question}} 
          <span v-if="required">*</span>
        </p>
        <p class="text-work-san f-20 opacity-50"> {{questionDesc}} </p>
        <v-row v-if="options.length==2" class="space-around">
          <v-col cols sm="5" v-for="(option,idx) of options" 
          :key="idx" @click="selectAns(idx)">
          <Button width="200" :height="option.pic?'150':'50'">
                <div>
                  <img v-if="option.pic" :src="option.pic" width="60%"/>
                  <p class="text-work-san f-18 mb-0" v-text="option.name"></p>  
                  <div v-if="(multiple && selected.includes(idx))||(!multiple && singleSelect==idx)"
                    class="d-flex align-start justify-end selected" :class="dark?'white':'grey darken-4'">
                    <v-icon :color="dark?'black':'white'">mdi-check</v-icon>
                  </div>
                </div>
            </Button>
          </v-col>
        </v-row>
        <v-row v-else-if="options.length==3" class="space-around">
          <v-col cols sm="4" v-for="(option,idx) of options" 
          :key="idx" @click="selectAns(idx)">
          <Button width="180" :height="option.pic?'145':'50'">
                <div>
                  <img v-if="option.pic" :src="option.pic" width="60%"/>
                  <p class="text-work-san f-18 mb-0" v-text="option.name"></p>  
                  <div v-if="(multiple && selected.includes(idx))||(!multiple && singleSelect==idx)"
                    class="d-flex align-start justify-end selected" :class="dark?'white':'grey darken-4'">
                    <v-icon :color="dark?'black':'white'">mdi-check</v-icon>
                  </div>
                </div>
            </Button>
          </v-col>
        </v-row>
        <v-row v-else-if="options.length>3 && options.length<=6 && !options[0].pic" class="space-around">
          <v-col cols sm="6" v-for="(option,idx) of options" 
          :key="idx" @click="selectAns(idx)">
          <Button width="250" :height="option.pic?'145':'50'">
                <div>
                  <img v-if="option.pic" :src="option.pic" width="60%"/>
                  <p class="text-work-san f-18 mb-0" v-text="option.name"></p>  
                  <div v-if="(multiple && selected.includes(idx))||(!multiple && singleSelect==idx)"
                    class="d-flex align-start justify-end selected" :class="dark?'white':'grey darken-4'">
                    <v-icon :color="dark?'black':'white'">mdi-check</v-icon>
                  </div>
                </div>
            </Button>
          </v-col>
        </v-row>
        <v-row v-else-if="options.length>3 && options.length<=6" class="space-around">
          <v-col v-for="(option,idx) of options" 
          :key="idx" @click="selectAns(idx)">
          <Button width="140" :height="option.pic?'145':'50'">
                <div>
                  <img v-if="option.pic" :src="option.pic" width="60%"/>
                  <p class="text-work-san f-18 mb-0" v-text="option.name"></p>  
                  <div v-if="(multiple && selected.includes(idx))||(!multiple && singleSelect==idx)"
                    class="d-flex align-start justify-end selected" :class="dark?'white':'grey darken-4'">
                    <v-icon :color="dark?'black':'white'">mdi-check</v-icon>
                  </div>
                </div>
            </Button>
          </v-col>
        </v-row>
        <!-- <div v-else-if="options.length>3 && options.length<=6 && !options[0].pic"
          class="d-flex flex-wrap ml-n5 ml-md-0">
          <v-col cols="5" v-for="(option,idx) of options" 
          :key="idx" 
          class="option pa-0 ma-md-3 mr-1 mb-1 "
          :class="`${selected==idx?'blink':''} option${dark?'Dark':'Light'}`"
          @click="selectAns(idx)">
            <v-card outlined class="transparent">
              <div class="d-flex align-center justify-center">
                <img :src="option.pic" width="50%"/>
              </div>
              <div class="d-flex ma-2">
                <v-card v-if="keyboardSelect" flat class="white black--text px-2 mr-2 rounded-sm">
                  <b class="text-work-san f-18">{{String.fromCharCode(65+idx)}}</b>
                </v-card>
                <p class="text-work-san f-18 mb-0" v-text="option.name"></p>
              </div>
            </v-card>
            <div v-if="(multiple && selected.includes(idx))||(!multiple && singleSelect==idx)"
            class="d-flex align-start justify-end selected" :class="dark?'white':'grey darken-4'">
              <v-icon :color="dark?'black':'white'">mdi-check</v-icon>
            </div>
          </v-col>
        </div> -->
        <!-- <div v-else-if="options.length>3 && options.length<=6" 
        class="d-flex flex-wrap space-around">
          <div v-for="(option,idx) of options" 
          :key="idx" 
          class="option pa-0 ma-md-3 mr-1 mb-1"
          :class="`${selected==idx?'blink':''} option${dark?'Dark':'Light'}`"
          @click="selectAns(idx)">
            <v-card outlined class="transparent">
              <div class="d-flex align-center justify-center">
                <img :src="option.pic" width="50%"/>
              </div>
              <div class="d-flex ma-2">
                <v-card v-if="keyboardSelect" flat class="white black--text px-2 mr-2 rounded-sm">
                  <b class="text-work-san f-18">{{String.fromCharCode(65+idx)}}</b>
                </v-card>
                <p class="text-work-san f-18 mb-0" v-text="option.name"></p>
              </div>
            </v-card>
            <div v-if="(multiple && selected.includes(idx))||(!multiple && singleSelect==idx)" 
            class="d-flex align-start justify-end selected" :class="dark?'white':'grey darken-4'">
              <v-icon :color="dark?'black':'white'">mdi-check</v-icon>
            </div>
          </div>
        </div> -->
        <div v-else-if="options.length>6">
          <v-autocomplete
            :items="options"
            item-text="name"
            placeholder="Type or select an option"
            class="text-work-san answer"
            color="black"
            item-color="black"
            :multiple="multiple"
          ></v-autocomplete>
        </div>
        
        <Button width="85" class="mt-4" @click="$emit('next');">
          <div class="d-flex">
            <p class="mb-0 grey--text text--darken-3 f-16">ok</p>
            <v-icon color="grey darken-3" class="ml-2">mdi-arrow-right-thin</v-icon>
          </div>
        </Button>
      </div>
    </div>
  </v-card>
</template>

<script>
import Button from '../Button.vue';
export default {
    name: "Mcq",
    props: {
        value: [String, Array],
        no: String,
        question: String,
        questionDesc: String,
        options: Array,
        keyboardSelect: {
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
    data() {
        return {
            selected: [],
            singleSelect: -1,
        };
    },
    methods: {
        selectAns(idx) {
            if (this.selected.includes(idx)) {
                var i = this.selected.indexOf(idx);
                this.selected.splice(i, 1);
            }
            else {
                this.selected.push(idx);
            }
            if (this.singleSelect == idx) {
                this.singleSelect = -1;
            }
            else {
                this.singleSelect = idx;
            }
            if (this.multiple) {
                this.updateValue(`${this.selected}`);
            }
            else {
                this.updateValue(`${this.singleSelect}`);
            }
        },
        key(e) {
            var keyPressed = (e.keyCode <= 90 ? e.keyCode + 32 : e.keyCode) - 97;
            this.selectAns(keyPressed);
        },
        updateValue(value) {
            this.$emit("input", value);
        }
    },
    components: { Button }
}
</script>

<style scoped>
.answer{
  font-size:20px;
}
.answer .v-select__slot{
  padding: 10px 0;
}
.selected{
  top:-1px;
  right:-1px;
  height:48px;
  width: 48px;
  border-radius: 5px;
  position: absolute;
  clip-path: polygon(0% 0, 100% 0, 100% 100%);
}
.f-18{
  font-size: 18px;
  line-height: 1;
}

@media (max-width: 480px) {
  .answer{
  font-size:16px;
  }
  .f-18{
  font-size:14px;
  }
}
</style>