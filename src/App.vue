<template>
  <v-app>

    
    <!-- TOOLBAR -->
  <div>
    <v-toolbar dark>
       <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
      <v-toolbar-title>Managment application with Vue.js</v-toolbar-title>
    </v-toolbar>
  </div>

        <!-- SIDE MENU -->

  <v-navigation-drawer 
    app 
    v-model="drawer" 
    color = "black"
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
        <v-btn color="success" block :to="{name: 'tasks'}"> TASKS </v-btn>
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
