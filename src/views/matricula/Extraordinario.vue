<template>
   
      <div >
        <div class="text-start">
         <p class="parrafo mt-2 ms-3">
           (Cómo entender el servicio de matricula)
            <a
              type="button"
              class="fuente tamanio ms-2"
              v-tooltip.bottom="
                'Mirar la demostración de el proceso de matriculas y generar los paralelos'
              "
            >
              <i class="fa fa-eye" aria-hidden="true"></i>
              <b class="links ms-1 me-2">Ver demostración</b>
            </a>
           
          </p>
      </div>
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
           
          </div>
        </section>
         
            <div v-if="ifCreateUpdate">
             <CreateMatricula2 :modalidad="mod"  @myEventClosedModalMatricula="closedChildMatricula" ></CreateMatricula2>
         </div>
          <div v-if="ifRemoveMatricula">
             <ListRemoveMatricula2 :modalidad="mod"  @myEventClosedModalRemove="closedChildRemoveMa2" ></ListRemoveMatricula2>
         </div>
         <div v-if="ifParalelo2">
             <ParaleloMatricula2  @myEventClosedModalParalelo2="closedChildParalelo2" ></ParaleloMatricula2>
         </div>
          <div v-if="ifMigracion">
          <MigracionMatricula @myEventClosedModalMigracion1="closedChildMigracion" :idGet="mod"></MigracionMatricula>
        </div>
        <div v-if="ifMigracion2">
          <MigrationnList
            @myEventClosedModalMigracion2="closedChildMigracionList"
          ></MigrationnList>
        </div>
      </div>
    
</template>

<script>
const img2 = require("../../assets/img/icons/pdf.png")
import RestResource from '../../service/isAdmin'
import fotos from '../../service/UploadsServices';
const restResourceService = new RestResource();
const restFotosService = new fotos();
const images = restFotosService.arrays_of_avatar();
import CardsOptions from "../../shared/CardsClick.vue"
export default {
  name: "Matriculas2",
  components: {
    CreateMatricula2: () =>
    import(
      /* webpackChunkName: "CreateMatricula2" */ "./pages/add/Add.vue"
    ),
    ListRemoveMatricula2: () =>
      import(
        /* webpackChunkName: "ListRemoveMatricula2" */ "./pages/list/List.vue"
      ),
      ParaleloMatricula2: () =>
      import(
        /* webpackChunkName: "EnlistarParalelom2" */ "./pages/paralelo2/Paralelo.vue"
      ),
      MigracionMatricula: () =>
      import(
        /* webpackChunkName: "MigracionMatricula" */ "./pages/migracion/Migracion.vue"
      ),
      MigrationnList: () =>
      import(
        /* webpackChunkName: "MigrationnList" */ "./pages/history/History.vue"
      ),
      CardsOptions
},
  data() {
    return {
      roles: this.$store.state.user.roles,
       //CHILD COMPONENT
      ifCreateUpdate: false,
      ifRemoveMatricula: false,
      ifParalelo2: false,
      ifMigracion: false,
      ifMigracion2: false,
      mod : 'm2',
      arrays_of_options: [
        {
          id: "0",
          nombre: "Matricular",
          img: images[0],
          description: "Puedes crear nueva matricula, la matricula es unica por cada estudiante",
        },
        
        {
          id: "2",
          nombre: "Paralelos",
          img: images[2],
          description: " Puede asignar, listar y remover paralelos en cada uno de los cursos",
        },
        {
          id: "1",
          nombre: "Reporte Matricula",
          img: img2,
          description: "Puede ver o eliminar la lista de los matriculados en el periodo",
        },
         {
          id: "3",
          nombre: "Respaldo",
          img: images[3],
          description: "Le permite generar copias de las matriculas y tambien limpiar la data",
        },
        {
          id: "4",
          nombre: "Historial Matricula",
          img: images[4],
          description: "Le permite revisar matriculas anteriores",
        },
      ]
    };
  },
  methods: {
    verificarUsuario(){
    let text_1 = 'Matriculas'
      let text_2 = 'Modalidad extraordinaria'
      this.$store.commit('updateHeader',{text_1, text_2})
      if(!restResourceService.admin(this.roles)){
        this.$router.push("/");
      }
    },
    optionsView: function(num){
      switch (num) {
        case 0:
          this.ifCreateUpdate = true;
          break;
        case 1:
        this.ifParalelo2 = true;
          break;
        case 2:
          
          this.ifRemoveMatricula = true;
          break;
        case 3:
          this.ifMigracion = true;
          break;
        case 4:
            this.ifMigracion2 = true;
            break;
        default:
          console.log("I don't own a pet");
          break;
      }
    },

    closedChildMatricula: function() {
      this.ifCreateUpdate = false;
    },
    closedChildRemoveMa2: function() {
      this.ifRemoveMatricula = false;
    },
    closedChildParalelo2: function() {
      this.ifParalelo2 = false;
    },
    closedChildMigracion: function() {
      this.ifMigracion = false;
    },
    closedChildMigracionList: function() {
      this.ifMigracion2 = false;
    },
  },
  created() {
    this.verificarUsuario();
  },

};

</script>
