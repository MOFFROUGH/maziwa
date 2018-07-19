<template>
  <v-app >
    <v-navigation-drawer
      v-model="drawer"
      fixed

      class="grey lighten-4 mt-5"
      width="250"
      app

      v-if="$store.state.isLoggedIn">
      <v-list dense class="grey lighten-4" >
        <template >
          <div>
            <v-subheader><h3 class="subheader_color">System User</h3></v-subheader>
               <v-list-tile @click="navigateTo('/')" >
                  <v-list-tile-action>
                      <v-icon>home</v-icon>
                  </v-list-tile-action>
                  <v-list-tile-content>
                    <v-list-tile-title>
                        Home
                   </v-list-tile-title>
                  </v-list-tile-content>
              </v-list-tile>

              <v-list-tile v-if="!$store.state.isLoggedIn" @click="navigateTo('login')" >
                  <v-list-tile-action>
                      <v-icon>fingerprint</v-icon>
                  </v-list-tile-action>
                  <v-list-tile-content>
                    <v-list-tile-title>
                        Login
                   </v-list-tile-title>
                  </v-list-tile-content>
              </v-list-tile>

              <v-list-tile v-if="!$store.state.isLoggedIn" @click="navigateTo('register')" >
                  <v-list-tile-action>
                      <v-icon>how_to_reg</v-icon>
                  </v-list-tile-action>
                  <v-list-tile-content>
                    <v-list-tile-title>
                        Register
                   </v-list-tile-title>
                  </v-list-tile-content>
              </v-list-tile>

              <v-list-tile @click="navigateTo('/dashboard')" >
                  <v-list-tile-action>
                      <v-icon>dashboard</v-icon>
                  </v-list-tile-action>
                  <v-list-tile-content>
                    <v-list-tile-title>
                        Dashboard
                   </v-list-tile-title>
                  </v-list-tile-content>
              </v-list-tile>

             <v-list-tile @click="" @click="logout">
                  <v-list-tile-action>
                      <v-icon>power_settings_new</v-icon>
                  </v-list-tile-action>
                  <v-list-tile-content>
                    <v-list-tile-title>
                        Logout
                   </v-list-tile-title>
                  </v-list-tile-content>
              </v-list-tile>
        </div>
          <!--- Other componets of adding farmer, cow, milk etc-->

          <v-divider dark class="my-3"></v-divider>
          <div>
            <v-subheader><h3 class="subheader_color">Farmer's Details</h3></v-subheader>
           <v-list-tile @click="navigateTo('/farmer')" >
                  <v-list-tile-action>
                   <div><img :src="require('@/assets/farmer.svg')" height="30"></div>
                  </v-list-tile-action>
                  <v-list-tile-content>
                    <v-list-tile-title>
                        Farmer
                   </v-list-tile-title>
                  </v-list-tile-content>
            </v-list-tile>
           <v-divider dark class="my-3"></v-divider>
           <v-subheader><h3 class="subheader_color">Cows' Profiles</h3></v-subheader>
            <v-list-tile @click="navigateTo('/cows')" >
                  <v-list-tile-action>
                 <div><img :src="require('@/assets/cow1.svg')" height="30" width="30"></div>
                  </v-list-tile-action>
                  <v-list-tile-content>
                    <v-list-tile-title>
                       Cows
                   </v-list-tile-title>
                  </v-list-tile-content>
            </v-list-tile>
            <v-divider dark class="my-3"></v-divider>
            <v-subheader>
              <h3 class="subheader_color">Cow details</h3>
            </v-subheader>
            <v-list-tile style="text-decoration:none;color:black;":to="item.to" v-for="item,i in sideNav" :key="i">
                  <v-list-tile-action>
                 <div>
                   <img :src="item.src" height="30" width="30">
                 </div>
                  </v-list-tile-action>
                  <v-list-tile-content>
                    <v-list-tile-title>
                       {{item.title}}
                   </v-list-tile-title>
                  </v-list-tile-content>
            </v-list-tile>
            <!-- <v-list-tile @click="navigateTo('/milk_records')" >
                  <v-list-tile-action>
                 <div><img :src="require('@/assets/milk-can.svg')" height="30"></div>
                  </v-list-tile-action>
                  <v-list-tile-content>
                    <v-list-tile-title>
                       Milk Records
                   </v-list-tile-title>
                  </v-list-tile-content>
            </v-list-tile>
            <v-list-tile @click="navigateTo('/inseminations')" >
                  <v-list-tile-action>
                 <div><img :src="require('@/assets/AI.svg')" height="30"></div>
                  </v-list-tile-action>
                  <v-list-tile-content>
                    <v-list-tile-title>
                       Insemination Records
                   </v-list-tile-title>
                  </v-list-tile-content>
            </v-list-tile>
            <v-list-tile @click="navigateTo('/births')" >
                  <v-list-tile-action>
                 <div><img :src="require('@/assets/cow-calf.svg')" height="30" width="30"></div>
                  </v-list-tile-action>
                  <v-list-tile-content>
                    <v-list-tile-title>
                       Birth Records
                   </v-list-tile-title>
                  </v-list-tile-content>
            </v-list-tile>
            <v-list-tile @click="navigateTo('/treatments')" >
                  <v-list-tile-action>
                 <div><img :src="require('@/assets/needle.svg')" height="30"></div>

                  </v-list-tile-action>
                  <v-list-tile-content>
                    <v-list-tile-title>
                       Treatment Records
                   </v-list-tile-title>
                  </v-list-tile-content>
            </v-list-tile>
            <v-list-tile @click="navigateTo('/vaccinations')" >
                  <v-list-tile-action>
                 <div><img :src="require('@/assets/needle.svg')" height="30"></div>
                  </v-list-tile-action>
                  <v-list-tile-content>
                    <v-list-tile-title>
                       Vaccinations
                   </v-list-tile-title>
                  </v-list-tile-content>
            </v-list-tile> -->
          </div>
        </template>
      </v-list>
    </v-navigation-drawer>
    <v-toolbar flat color="green" app  clipped-left v-if="!l">
      <v-toolbar-side-icon v-if="$store.state.isLoggedIn" @click.native="drawer = !drawer"></v-toolbar-side-icon>
      <span class="title ml-3 mr-5">Dairy Analytics</span>
      <v-spacer></v-spacer>
      <v-toolbar-items class="hidden-sm-and-down">
          <v-btn flat to="/">Home</v-btn>
          <v-btn flat v-if="!$store.state.isLoggedIn" to="/register">Register</v-btn>
          <v-btn flat v-if="!$store.state.isLoggedIn" to="/login">Login</v-btn>
          <v-btn v-if="$store.state.isLoggedIn" flat to="/dashboard">Dashboard</v-btn>
    </v-toolbar-items>
    </v-toolbar>
    <v-content>
      <v-container  fluid  fill-height>
        <v-layout row wrap>
          <v-flex xs12>
             <router-view></router-view>
          </v-flex>
        </v-layout>
      </v-container>
    </v-content>
    <v-footer app fixed>
       <span>&copy; Bart</span>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  methods:{
    navigateTo(route){
      this.$router.push(route)
      //console.log('pressed',route)
    },
    logout(){
      this.$store.dispatch('setToken',null)
      this.$store.dispatch('setUser',null)
      this.$router.push('/')
      this.$localStorage.remove('token')
    }
  },
  data(){
    return{
      drawer:false,
      sideNav: [
        {to: '/cows', src: '/static/AI.svg', title: 'Cows' },
        {to: '/cows', src: '/static/AI.svg', title: 'Cows' },
        {to: '/cows', src: '/static/AI.svg', title: 'Cows' },
        {to: '/cows', src: '/static/AI.svg', title: 'Cows' }
      ]
    }
  },
  computed: {
    l () {
      if(this.$store.state.isLoggedIn){
        return false
      }
      if(this.$route.path == '/register' ||this.$route.path=='/login'){
         return false
       }else{
         return  true
       }
    }
  }

}
</script>

<style>
 .subheader_color{
   color: green;
   /* color:rgb(129, 199, 132) !important; */
 }
</style>
