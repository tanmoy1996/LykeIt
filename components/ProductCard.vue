<template>
  <v-hover v-slot="{ hover }">
    <v-card 
    :class="hover?'bounce':null"
    class="prodCard rounded-lg">
      <div class="logo">
        <img :src="product.logo"/>
      </div>
      <v-card flat class="transparent pa-3 pt-10">
        <v-card-text class="text-center">
          <h2 v-text="product.name"></h2>
          <p v-text="product.desc"></p>
        </v-card-text>
        <v-card-text>
          <v-row>
            <v-col cols="6" class="text-center">
              <h1>24</h1>
              <v-divider class="ma-3"></v-divider>
              <p>Likes</p>
            </v-col>
            <v-divider vertical class="my-3"></v-divider>
            <v-col cols="6" class="text-center">
              <h1>45</h1>
              <v-divider class="ma-3"></v-divider>
              <p>Comments</p>
            </v-col>
          </v-row>
        </v-card-text>
        <div class="d-flex justify-center">
          <v-rating
          v-model="product.rating"
            color="amber"
            half-increments
            length="5"/>
        </div>
      </v-card>
      <v-divider></v-divider>
      <v-card-actions class="pa-0">
        <v-btn block 
        :dark="hover"
        :class="hover?'grad':null"
        class="py-6 rounded-b-lg">
          Check Analytics
        </v-btn>
      </v-card-actions>
    </v-card>
  </v-hover>
</template>

<script>
export default {
    name:"ProductCard",
    props:['product'],
}
</script>

<style scoped>
.prodCard{
  transition: all cubic-bezier(0, 0.01, 0.13, 2.46) 300ms;
}
.logo{
  position: absolute;
  top:-50px;
  left:calc(50% - 40px);
}
.logo img{
  height:80px;
  width:80px;
  object-fit: cover;
  border-radius: 50%;
  box-shadow: 1px 1px 10px -2px #555;
}
.bounce{
  transform: translateY(-20px);
}
</style>