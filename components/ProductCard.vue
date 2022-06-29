<template>
  <Button width="255" height="310">
    <v-card flat class="transparent" width="250">
      <v-row class="pa-0 ma-0">
        <v-col cols="4">
          <nuxt-img :src="product.logo" class="logo"></nuxt-img>
        </v-col>
        <v-col cols="8" class="d-flex align-center">
          <div class="ml-2 grey--text text--darken-3">
            <h4 v-text="product.name"></h4>
            <p class="mb-0 f-14" v-text="product.desc"></p>
          </div>
        </v-col>
      </v-row>
      <div class="d-flex align-center h-100 grey lighten-2 mx-2 rounded">
        <v-card-text>
          <p v-if="product.lastReview" class="review">{{product.lastReview}}</p>
          <p v-else class="text-center">No reviews yet</p>
        </v-card-text>
      </div>
      <v-card-text class="py-0 px-2 d-flex justify-space-between">
        <v-btn depressed class="grey lighten-2 text-lowercase pa-1 mt-1">
          http://taplyk/125dS47
        </v-btn>
        <v-btn depressed class="mt-1 pa-1">
          <nuxt-img src="/qr.jpg" width="30"></nuxt-img>
        </v-btn>
      </v-card-text>
      <v-card-text class="pa-0 d-flex justify-center">
        <v-rating
          v-model="product.rating"
          color="amber"
          readonly
          half-increments
          length="5"/>
      </v-card-text>
      <v-card-actions class="pb-0">
        <v-spacer></v-spacer>
        <p class="pb-0 text-work-san underline">Go to Analytics
          <v-icon small class="mt-n1">mdi-arrow-right</v-icon>
        </p>

      </v-card-actions>
    </v-card>
  </Button>
</template>

<script>
import Button from './Button.vue';
export default {
    name: "ProductCard",
    props: ["product"],
    components: { Button }
}
</script>

<style scoped>

.logo{
  height:70px;
  width:70px;
  object-fit: cover;
  border-radius: 50%;
  border: 2px solid rgb(32, 32, 32);
}

.review{
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  overflow: hidden;
  font-style: italic;
}
.review:before {
  content: open-quote;
}
.review:after {
  content: close-quote;
}
.review:before,
.review:after {
  display: inline-block;
  vertical-align: bottom;
  color: orange;
  font-size: 2em;
  top: .2em;
  position: relative;
  padding:0 2px;
}
.h-100{
  height:90px;
}
.underline{
  border-bottom: 2px solid #ffd05c;
}
</style>