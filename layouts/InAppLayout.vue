<template>
  <v-app>
    <v-main>
      <v-app-bar
        flat
        class="transparent"
        hide-on-scroll>
        <h2 >tap</h2>
        <Button width="45" height="35">
          <h2 class="f-16">lyk</h2>
        </Button>
        <v-spacer></v-spacer>
        <div class="d-none d-md-flex">
          <Button width="250" height="42" class="mx-2">
            <v-text-field
              solo
              flat
              dense
              hide-details
              color="black"
              label="Search Product"
              prepend-inner-icon="mdi-magnify"
              />
          </Button>
          <v-avatar>
            <img src="https://cdn.vuetifyjs.com/images/john.jpg" alt="Profile Pic">
          </v-avatar>
        </div>
        <!-- menu -->
        <v-btn icon class="d-flex d-md-none">
          <v-icon>mdi-menu</v-icon>
        </v-btn>
      </v-app-bar>
      <v-container fluid class="my-0">
        <Nuxt />
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import Button from '~/components/Button.vue';
export default {
    name: "InAppLayout",
    components: { Button },
    data() {
        return {
            name: "AV Avijit",
        };
    },
    
}
</script>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Work+Sans&display=swap');
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
  .f-32{
  font-size: 32px;
  }
  .opacity-50{
    opacity: 0.5;
  }
  .no-outline{
    outline:none;
  }
</style>
<style scoped>
.li-search-width{
  width:300px;
}
</style>