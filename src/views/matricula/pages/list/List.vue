<template>
  <ScrimModal @close="close">
    <template v-slot:header> Lista de matriculas actuales</template>
    <template v-slot:body>
      <Spinner v-if="isLoading1"></Spinner>
      <section v-else>
        <Dropdown v-model="curso" :options="listniveles" />
        <Astronauta v-if="isPrint" />
        <Spinner v-if="isTabla"></Spinner>
        <section v-else>
          <div v-if="infoMat.length" class="mt-3">
            <div class="row mb-2">
              <div class="col-lg-4">
                <div class="input-group" style="margin-bottom: 7px;">
                  <span class="input-group-text text-body buscador"><i class="fas fa-search links"
                      aria-hidden="true"></i></span>
                  <input class="form-control buscador" type="text" v-model="searchQuery" style="background: white;"
                    placeholder="Buscar">
                </div>
              </div>
              <div class="col-lg-8 text-end">


                <a class="fuente tamanio negros me-3" role="button" @click="get2()">
                  <svg class=" me-1" data-testid="geist-icon" fill="none" height="20"
                    shape-rendering="geometricPrecision" stroke="currentColor" stroke-linecap="round"
                    stroke-linejoin="round" stroke-width="1.5" viewBox="0 0 24 24" width="20"
                    style="color:#000;margin-top: -3px;">
                    <path d="M2 3h6a4 4 0 014 4v14a3 3 0 00-3-3H2z"></path>
                    <path d="M22 3h-6a4 4 0 00-4 4v14a3 3 0 013-3h7z"></path>
                  </svg>
                  Promoción
                </a>
                <a class="fuente tamanio negros" role="button" @click="get()">
                  <svg class=" me-1" data-testid="geist-icon" fill="none" height="20"
                    shape-rendering="geometricPrecision" stroke="currentColor" stroke-linecap="round"
                    stroke-linejoin="round" stroke-width="1.5" viewBox="0 0 24 24" width="20"
                    style="color:#000;margin-top: -3px;">
                    <path d="M6 9V2h12v7"></path>
                    <path d="M6 18H4a2 2 0 01-2-2v-5a2 2 0 012-2h16a2 2 0 012 2v5a2 2 0 01-2 2h-2"></path>
                    <path d="M6 14h12v8H6z"></path>
                  </svg>
                  Matriculas
                </a>
              </div>
            </div>
            <div class="table-responsive">
              <table class="dataTable-table table s-table-flush">
                <thead class="thead-light">
                  <tr class="cabeza">
                    <th style="background-color: rgb(234, 240, 246); ">
                      <div class="d-flex ms-3">
                        <div v-if="!allSelected" class="form-check my-auto" style="min-height: 0rem;">
                          <input class="form-check-input cheka" type="checkbox" @click="selectAll" />
                        </div>
                        <i @click="deletedSelected" v-else class="fa fa-minus s-icon-all" aria-hidden="true"></i>
                        <span class="ms-3 text-uppercase text-center text-xxs font-weight-bolder">
                          Nombres
                        </span>
                      </div>
                    </th>
                    <th class="text-uppercase text-center text-secondary text-xxs font-weight-bolder opacity-7">
                      Paralelo
                    </th>
                    <th class="text-uppercase text-center text-secondary text-xxs font-weight-bolder opacity-7">
                      Fecha
                    </th>

                  </tr>
                </thead>
                <tbody>
                  <tr v-for="item in displayedArticles" :key="item.id"
                    :class="{ 's-ifactive': isSelecMatricula.includes(item._id) }">
                    <td>
                      <div class="d-flex ms-3">
                        <div class="form-check my-auto supcheka">
                          <input class="form-check-input cheka" type="checkbox" v-model="isSelecMatricula"
                            :value="item._id" @click="selectcursos(item._id)" />
                        </div>
                        &nbsp;&nbsp;
                        <span class="mb-0 mt-1 text-xs negros fuente">
                          {{ item.nombre }}
                        </span>
                      </div>
                    </td>
                    <td class="text-xs text-center text-dark fuente">
                      {{ item.curso }}
                    </td>
                    <td class="text-xs text-center text-dark fuente">
                      {{ item.fecha }}
                    </td>

                  </tr>
                </tbody>
              </table>
              <Paginate :numPages="numPages" :page="page" :total="infoMat.length" @pagechanged="onPageChange">
              </Paginate>
            </div>
          </div>
          <section v-else>
            <NoFound />
          </section>
        </section>
        <section v-if="ifmatricula">
          <FormatoMatricula :rowData="rowData" @changeStatus="changeStatus" />
        </section>
      </section>
    </template>
    <template v-slot:footer>
      <a style="text-decoration: underline;" href="javascript:;" class="fuente tamanio links me-3" @click="verLista()">
        <b>Salir de aqui</b>
      </a>
    </template>
  </ScrimModal>
</template>
<script>
import Spinner from "../../../../shared/Spinner.vue";
import ScrimModal from "../../../../shared/ScrimModal"
import Paginate from "../../../../shared/Paginate.vue";
import Dropdown from "../../../../shared/Dropdown.vue";
import NoFound from "../../../../shared/NoFound"
import Astronauta from "../../../../shared/Astronauta";
export default {
  name: "ListaMatricula",
  components: {
    //Espera,
    Spinner, ScrimModal, Paginate, NoFound, Dropdown, Astronauta,
    FormatoMatricula: () => import( /* webpackChunkName: "FormatoMatricula" */ "../reportes/FormatoMatricula.vue"),
  },
  props: {
    modalidad: {
      type: String,
    }
  },
  data() {
    return {
      isLoading1: false,
      isTabla: false,
      listPeriodo: null,
      check: null,
      select: null,
      infoMat: {},
      listniveles: null,
      isSelecMatricula: [],
      iseliminaddo: false,
      nombre_curso: "",
      index: "0",
      isPrint: false,
      arrays: [],
      //PAGINATE 
      searchQuery: '',
      //Pagina 
      page: 1,
      perPage: 9,
      pages: [],
      numPages: 0,
      totalNotas: 0,
      allSelected: false,
      curso: '',
      idCurso: '',
      ifmatricula: false,
    };
  },
  computed: {
    displayedArticles: function () {
      if (this.searchQuery.length > 1) {
        return this.infoMat.filter((item) => {
          return this.searchQuery
            .toLowerCase()
            .split(" ")
            .every((v) => item.nombre.toLowerCase().includes(v));
        });
      } else {
        return this.paginate(this.infoMat);
      }

    }
  },
  watch: {
    curso: function (value) {
      this.idCurso = value._id
      this.__cambios(this.idCurso);
    }
  },
  methods: {//Extraordinaria
    paginate(articles) {
      let page = this.page;
      let perPage = this.perPage;
      let from = (page * perPage) - perPage;
      let to = (page * perPage);

      this.numPages = Math.ceil(articles.length / 8);
      return articles.slice(from, to);
    },
    get: function () {
      if (this.isSelecMatricula.length > 0) {
        this.ifmatricula = false
        this.isPrint = true;
        this.rowData = this.isSelecMatricula
        setTimeout(() => this.callReport(), 150);
      } else {
        this.$dialog.alert("Selecione un estudiante por lo menos");
      }
    },
    get2(){
      alert("AUN NO ESTA EN FUNSIÓN");
    },
    changeStatus(ev) {
      if (ev == '100') {
        this.isPrint = false;
      }
    },
    callReport() {
      if (this.rowData.length > 0) this.ifmatricula = true
      if (this.rowData.length == 0) this.isPrint = false;
    },
    verificarUsuario() {
      if (this.modalidad == 'm1') {
        this.isOptionsModalidad = 'Intensivo';
      }
      if (this.modalidad == 'm2') {
        this.isOptionsModalidad = 'Extraordinaria';
      }
      this.__listNivele();

    },
    onPageChange: function (page) {
      this.page = page;
    },
    __listNivele() {
      //-----------TRAE LA LISTA DE LOS ROLES
      this.isLoading1 = true;

      this.$proxies._gestionProxi
        .getNiveles()
        .then((x) => {
          let filtros = x.data;
          this.listniveles = filtros.filter((x) => x.modalidad == this.isOptionsModalidad);
          // this.isTabla = false;
          this.isLoading1 = false;
        })
        .catch((err) => {
          console.log("Error", err);
          // this.isTabla = false;
          this.isLoading1 = false;
        });
    },
    __cambios(cursos) {
      this.isTabla = true;
      this.$proxies._matriculaProxi
        .getFullMatricula(cursos)
        .then((x) => {
          this.infoMat = x.data.matriculados;
          this.isTabla = false;
        })
        .catch((err) => {
          console.log("Error", err);
          this.isTabla = false;
        });
    },

    selectcursos(ids) {

      if (!this.isSelecMatricula.includes(ids)) {
        this.isSelecMatricula.push(ids);
      } else {
        this.isSelecMatricula.splice(this.isSelecMatricula.indexOf(ids), 1);
      }
    },
    selectAll: function () {
      this.allSelected = true;
      this.isSelecMatricula = [];
      if (this.allSelected) {
        for (let user in this.infoMat) {
          this.isSelecMatricula.push(this.infoMat[user]._id);
        }
      }
    },
    deletedSelected: function () {
      this.allSelected = false;
      this.isSelecMatricula = [];
    },




    close() {
      this.$emit('myEventClosedModalRemove');
    },
  },
  created() {
    this.verificarUsuario();
  },

};
</script>