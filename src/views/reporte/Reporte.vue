<template>
    <div >
      <div class="text-start">
         <p class="parrafo mt-2 ms-3">
           (Cómo entender el servicio de reportes)
            <a
              type="button"
              class="fuente tamanio ms-2"
              v-tooltip.bottom="'Mirar la demostración de el proceso de matriculas y generar los paralelos'">
              <i class="fa fa-eye" aria-hidden="true"></i>
              <b class="links ms-1 me-2">Ver demostración</b>
            </a>
          </p>
      </div>
        
      <div class="row">
         <section class="intro_cards mt-3">
          <div class="intro_cards_container">
            <div  v-for="(item, i) in arrays_of_options" :key="item.id" class="intro_card_container"  >
              <CardsOptions :index="i"  :img="item.img" :nombre="item.nombre" :description="item.description" @optionsFuntions="optionsView"></CardsOptions>
            </div>
            <div class="intro_card_container" >
               <div class="carmen align_center animate__animated animate__fadeInUp animations-5">
                  <i class='bx bx-folder-plus p-5' style="font-size:60px;color:black;"></i>
              </div>
            </div>
            <div class="intro_card_container" >
               <div class="carmen align_center animate__animated animate__fadeInUp animations-5">
                  <i class='bx bx-folder-plus p-5' style="font-size:60px;color:black;"></i>
              </div>
            </div>
            <div class="intro_card_container" >
               <div class="carmen align_center animate__animated animate__fadeInUp animations-5">
                  <i class='bx bx-folder-plus p-5' style="font-size:60px;color:black;"></i>
              </div>
            </div>
          </div>
        </section>
      </div>
         <div v-if="ifConsolidado">
             <Consolidado  @myEventClosedModalConsolidado="closedChildConsolidado" ></Consolidado>
         </div>
    </div>
</template>

<script>
import RestResource from "../../service/isAdmin";
const restResourceService = new RestResource();
const img1 = require("../../assets/img/shapes/90260b20-d6c6-418f-9961-9282c5d85d78.png")
const img3 = require("../../assets/img/logs/add-on-reporting.svg")
const img4 = require("../../assets/img/logs/documents.svg")
import CardsOptions from "../../shared/CardsClick.vue"
export default {
  name: "MenuZonas",
 
  data() {
    return {
      roles: this.$store.state.user.roles,
      ifReportPdf: false,
      ifConsolidado : false,
      arrays_of_options: [
        {
          id: "0",
          nombre: "Consolidado",
          img: img1,
          description: "Puedes crear nuevos registros de provincias segun sea necesario ",
        },
       
        {
          id: "2",
          nombre: "Notas",
          img: img3,
          description: "Puedes crear nuevos registros de Notas segun sea necesario ",
        },
         {
          id: "3",
          nombre: "Permisos",
          img: img4,
          description: "Puedes crear nuevos registros de Permisos segun sea necesario ",
        },
       
      ]
    };
  },
  components:{
     Consolidado: () => import( /* webpackChunkName: "Consolidado" */ "./pages/consolidado/Consolidado.vue"),
      CardsOptions
  },
  methods: {
    verificarUsuario() {
        let text_1 = 'Matriculas'
      let text_2 = 'Reportes y consolidado'
      this.$store.commit('updateHeader',{text_1, text_2})
      if (!restResourceService.admin(this.roles)) {
        this.$router.push("/");
      }
    },
    optionsView: function(num){
      if (num===0) {
         this.ifConsolidado = true;
      }
      if (num===1) {
         this.ifReportPdf = true;
      }
    },
    closedChildReportPdf: function() {
      this.ifReportPdf = false;
    },
    closedChildConsolidado: function() {
      this.ifConsolidado = false;
    },
  },
  created() {
    this.verificarUsuario();
  },
};
</script>

