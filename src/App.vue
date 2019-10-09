<template>
  <v-app>
    <!-- TOOLBAR -->
<div>
    <v-toolbar app src="https://cdn.vuetifyjs.com/images/backgrounds/bg-2.jpg">
       <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
      <v-toolbar-title>Managment task application with Vue.js</v-toolbar-title>

      <div class="flex-grow-1"></div>

      <v-toolbar-items>
        <v-btn text>Link 1</v-btn>
        <v-btn text>Link 2</v-btn>
        <v-btn text>Link 3</v-btn>
      </v-toolbar-items>

      <template v-if="$vuetify.breakpoint.smAndUp">
        <v-btn icon>
          <v-icon>mdi-export-variant</v-icon>
        </v-btn>
        <v-btn icon>
          <v-icon>mdi-delete-circle</v-icon>
        </v-btn>
        <v-btn icon>
          <v-icon>mdi-plus-circle</v-icon>
        </v-btn>
      </template>
    </v-toolbar>
  </div>

        <!-- SIDE MENU -->

    <v-navigation-drawer 
    app 
    v-model="drawer" 
    src="https://cdn.vuetifyjs.com/images/backgrounds/bg-2.jpg"
    temporary 
    >

    <v-layout mt-4 column align-center>
      <v-flex>
        <v-avatar>
          <v-img src="https://randomuser.me/api/portraits/women/1.jpg"></v-img>
        </v-avatar>
      </v-flex>

      <v-flex>
        <p class="white--text mt-3 headline">Random user</p>
      </v-flex>
    </v-layout>

    <v-layout column>
      <v-flex mx-3>
        <v-btn color="success" block :to="{name: 'home'}"> HOME </v-btn>
        <br>
        <v-btn color="success" block :to="{name: 'tasks'}"> TASKS LIST </v-btn>
      </v-flex>
    </v-layout>

     
    </v-navigation-drawer>

    

    <v-content>
      <router-view/>
    </v-content>
  </v-app>
</template>

<script>


export default {
  name: 'App',
  components: {
    
  },
  data: () => ({
   drawer: true
  }),
};
</script>
