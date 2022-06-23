<template>
  <v-app >
    <Navbar :drawer="drawer"/>
    <v-app-bar fixed app flat class="blue lighten-5">
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />
      <v-toolbar-title class="text-dec" v-text="title" />
    </v-app-bar>
    <v-main class="blue lighten-5">
      <v-container fluid class="my-0">
        <Nuxt />
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import Navbar from '~/components/Navbar.vue'
export default {
    name: "InAppLayout",
    data() {
      return {
        drawer:true,
        title: "Dashboard",
        
      };
    },
    components: { Navbar }
}
</script>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Berkshire+Swash&display=swap');
  @import url('https://fonts.googleapis.com/css2?family=Work+Sans&display=swap');
  .grad{
    background-image: linear-gradient(122deg, rgba(2,0,36,1) 0%, rgba(9,9,116,1) 61%, rgba(17,91,205,1) 100%);
  }
  .full-screen{
    min-height: calc(100vh - 88px);
  }
  .text-work-san{
    font-family: 'Work Sans', sans-serif;
  }
  .f-24{
    font-size: 24px;
  }
  .f-20{
    font-size:20px;
  }
  .opacity-50{
    opacity: 0.5;
  }
</style>
<style scoped>
.text-dec{
  font-family: 'Berkshire Swash', cursive;
  font-size: 32px;
}

</style>