<template>
    <div >
       <div class="row">
         <section class="intro_cards mt-3">
          <div class="intro_cards_container">
            <div  v-for="(item, i) in arrays_of_options" :key="item.id" class="intro_card_container"  >
              <CardsOptions :index="i" :ruta="item.ruta" :img="item.img" :nombre="item.nombre" :description="item.description"></CardsOptions>
            </div>
            <div class="intro_card_container" >
               <div class="carmen align_center animate__animated animate__fadeInUp animations-5">
                  <i class='bx bx-folder-plus p-5' style="font-size:60px;color:black;"></i>
              </div>
            </div>
          </div>
        </section>
      </div>
    </div>
</template>
<script>
import RestResource from '../../service/isAdmin';
const restResourceService = new RestResource();
const img1 = require("../../assets/img/logs/map.svg")
const img2 = require("../../assets/img/usados/zonas.svg")
const img3 = require("../../assets/img/logs/bot-avatar.webp")
const img4 = require("../../assets/img/logs/grupo.svg")
import CardsOptions from "../../shared/CardsOptions.vue"
export default {
  name: "MenuZonas",
   components: {
    CardsOptions
  },
  data() {
    return {
      roles: this.$store.state.user.roles,
      arrays_of_options: [
        {
          id: "0",
          nombre: "Provincias",
          ruta: '/Provincias',
          img: img1,
          description: "Puedes crear nuevos registros de provincias segun sea necesario ",
        },
        {
          id: "1",
          nombre: "Cantones",
          ruta: '/Canton',
          img: img1,
          description: "Puedes crear nuevos registros de cantones segun sea necesario ",
        },
        {
          id: "2",
          nombre: "Parroquias",
          ruta: '/Parroquia',
          img: img2,
          description: "Puedes crear nuevos registros de parroquias segun sea necesario ",
        },
         {
          id: "3",
          nombre: "Nacionalidad",
          ruta: '/Nacionalidad',
          img: img3,
          description: "Puedes crear nuevos registros de nacionalidad segun sea necesario ",
        },
        {
          id: "4",
          nombre: "Etnia",
          ruta: '/Etnias',
          img: img4,
          description: "Puedes crear nuevos registros de etnias segun sea necesario ",
        },
      ]
    }
  },
  methods: {
     verificarUsuario(){
      let text_1 = 'Zonas'
      let text_2 = 'Información general'
      this.$store.commit('updateHeader',{text_1, text_2})
       if(!restResourceService.admin(this.roles)){
         this.$router.push("/");
       }
     }
  },
  created() {
    this.verificarUsuario();
  },
};
</script>