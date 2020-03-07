<template>
    <v-card
    color="grey lighten-4"
    flat
    tile
  >
    <v-toolbar extended extension-height="10">
      <!--<v-app-bar-nav-icon></v-app-bar-nav-icon>-->

      <v-toolbar-title>ChitChat</v-toolbar-title>

      <v-spacer></v-spacer>

     <div class="hidden-sm-and-down">
         <v-btn text>Forum</v-btn>
         <v-btn text>Pertanyaan</v-btn>
         <v-btn text>Kategori</v-btn>

         <router-link to="/login">
           <v-btn text>Login</v-btn>
         </router-link>

     </div>
    </v-toolbar>
    </v-card>

</template>

<script>
export default {
    
}
</script>

<style lang="">
    
</style>