<template>
  <div id="app" >
    <template v-if="hasConfig">
      <div v-if="isLoggedIn">

        <Header v-if="!$store.state.isAppMobile"></Header>
         <AppMovile v-else/>
        <main
          class="main-content position-relative  h-10 border-radius-lg "
          
        >
          <!-- Navbar -->
          <Inicio />
          <!-- End Navbar -->
          <div class="container-fluid  py-2" v-bind:style= "[$store.state.isAppMobile ? {'padding-bottom':'55px !important'} : {'padding-bottom':'.5rem !important'}]">
           <router-view/>
            <!-- INICIO FOOTER -->
            <!-- <Footer /> -->
           
            <!-- FIN FOOTER -->
          </div>
        </main>
        
      </div>
      <Login v-else />
    </template>
    <div v-else class="text-center" style="margin-top:300px; font-size:25px;">
      <p>Estamos cargando...</p>
    </div>
  </div>
</template>

<script>
import Header from "@/shared/Header.vue";
import Inicio from "@/shared/Inicio.vue";
//import Footer from "@/shared/Footer.vue";
import Login from "./views/auth/Login.vue";

export default {
  name: "app",
  mounted() {
    this.initialize();
  },
  components: {
    Header,
    Login,
    Inicio,
    //Footer,
    AppMovile : () => import( /* webpackChunkName: "AppMovile" */ '../src/shared/AppMovile.vue')
  },
  data() {
    return {
      hasConfig: false,
      isLoggedIn: false,
    };
  },
  methods: {
    initialize() {//https://pcei-tulcan.com http://localhost:3000/
      let self = this;
      if (!localStorage.getItem("config")) {
        var url = "https://pcei-tulcan.com/api";
        localStorage.setItem("config", JSON.stringify(url));
        self.hasConfig = true;
       // window.location.reload(true);
      } else {
        self.hasConfig = true;
        __isLogedIn();
      }
      function __isLogedIn() {
        if (localStorage.getItem("access_token") != null) {
          self.$user.initialize();
          self.isLoggedIn = true;
        }
      }
    },
  },
};
</script>
<style>
  @import './assets/styles/mainstyles.css';
</style>
