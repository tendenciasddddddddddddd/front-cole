<template>
    <div>
      <AlertHeader :firsttext="'Gestionar distributivo'" :lasttext="'Crea, edita, elimina y filtra'"></AlertHeader> 
       <ActionsRow :longitude="isSelecUsers.length"  @remove="remove" @gets="gets" @openModal="openModal" @openModalh="openAgGrid"/>
        <Spinner v-if="isLoading"></Spinner>
        <div v-else >
          <div v-if="!info.length" >
            <div class="row mt-2">
              <div class="col-lg-12">
                <div class="text-center">
                  <img
                    class="w-15"
                    src="../../../assets/img/logs/lupa.svg"
                    alt="fondo"
                  />
                  <div class="letra fuente mt-3">
                    No hay datos que mostrar
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div v-else>
          <div  class="table-responsive mt-2">
            <table class="dataTable-table table s-table-flush">
              <thead class="thead-light">
                <tr class="cabeza">
                  <th style="background-color: rgb(234, 240, 246); "
                  >
                   <div class="d-flex ms-3">
                      <div v-if="!allSelected " class="form-check my-auto" style="min-height: 0rem;">
                        <input
                          class="form-check-input cheka"
                          type="checkbox"
                          @click="selectAll"
                        />
                      </div>
                       <i @click="deletedSelected" v-else class="fa fa-minus s-icon-all" aria-hidden="true"></i>
                      <span class="ms-3 text-uppercase text-center text-xxs font-weight-bolder">
                       Curso / Paralelo
                      </span>
                    </div>
                  </th>
                   <th
                    class="text-uppercase  text-xxs font-weight-bolder">
                    Materia
                  </th>
                  <th
                    class="text-uppercase text-center text-xxs font-weight-bolder">
                    Docente
                  </th>
                   <th
                    class="text-uppercase text-center text-xxs font-weight-bolder">
                    Planificación
                  </th>
                </tr>
              </thead>

              <tbody>
                <tr v-for="item in info" :key="item.id">
                  <td>
                  <div class="d-flex ms-3">
                    <div class="form-check my-auto supcheka">
                      <input
                        class="form-check-input cheka"
                        type="checkbox"
                         v-model="isSelecUsers" :value="item._id"
                          @click="selectOne(item._id)"
                      />
                    </div>

                    <div class="mb-0 ms-3 text-xs colorestabla fuente">
                     <span v-if="item.fnivel">{{ item.fnivel.nombre }}</span> 
                     <span v-else class="text-danger ">Elimine este resgistro</span>
                      / {{ item.paralelo }}
                      <div>
                     
                    </div>
                    </div>
                  </div>
                </td>
                 <td class="text-xs  text-dark fuente">
                   <span class="UIStatusDot-sc-1axnt8y-0 cqKvgt" style="background-color: rgb(0, 189, 165);"
                        ></span> <span v-if="item.fmateria">{{ item.fmateria.nombre }} </span>  <span v-else class="text-danger ">Elimine este resgistro</span>
                </td>
                  <td class="text-xs text-center text-dark fuente">
                    <span > {{ item.fdocente ? item.fdocente.fullname:'Undefined' }} </span>
                   
                </td>
                 <td class="text-sm text-center text-dark fuente">
                  <div v-if="item.planificacion!==''">
                    <span style="background-color: rgb(0, 189, 165);" class="UIStatusDot-sc-1axnt8y-0 cqKvgt"></span>
                   <a :href="item.planificacion" target="_blank">Entregado</a> 
                  </div>
                  <div v-else>
                    <span class="UIStatusDot-sc-1axnt8y-0 cqKvgt"></span>
                   Sin entrega
                  </div>
                </td>
                </tr>
              </tbody>
            </table>
              <Paginate2 :numPages="paginas"  :page="pagina" :total="totalNotas" :subtitulo="subtitulo" @pagechanged="onPageChange" @setChangedQuery="changedQuery"></Paginate2>
          </div>
          </div>
        </div>
       <Modal v-show="visible" @close="close">
          <template v-slot:header> Distributivo Intensivo</template>
          <template v-slot:body>
             <Spinner v-if="isCarga"></Spinner>
                <form @submit.prevent="save" id="prov">
                   <span class="parrafo">Docente</span>
            <IsSelect v-if="isDocente"></IsSelect>
            <v-select class="style-chooser" placeholder="Selecionar docente"
              v-else
              :options.sync="listDocentes"
              label="fullname"
              v-model="selecDocente"
              required
            >
              <template #option="{ fullname }">
                <h6 style="margin: 0">{{ fullname }}</h6>
              </template>
              <template #no-options="{ }">
                Lo siento, no hay opciones de coincidencia.
              </template>
            </v-select>
            <p class="mb-2 text-sm text-danger">
              {{ validation.firstError("selecDocente") }}
            </p>
            <span class="parrafo">Paralelo</span>
            <Dropdown v-model="selecParalelos"  :options="paralelos"/>
            <p class="mb-2 text-xs text-danger">
              {{ validation.firstError("selecParalelos") }}
            </p>

                  <span class=" parrafo">Curso</span>
            <IsSelect v-if="isCurso"></IsSelect>
            <Dropdown v-model="model.fnivel"  v-else :options="listniveles"/>
            <p class="mb-2 text-xs text-danger">
              {{ validation.firstError("model.fnivel") }}
            </p>

            <span class="parrafo">Materia</span>
             <IsSelect v-if="isMateria"></IsSelect>
            <Dropdown v-model="model.fmateria"  v-else :options="listMaterias"/>
            <p class="mb-0 text-sm text-danger">
              {{ validation.firstError("model.fmateria") }}
            </p>
              
                </form>
          </template>
          <template v-slot:acccion>
            <ButtonLoading v-if="ifLoad"/>
                      <button form="prov" v-else type="submit" class="btn btnNaranja mt-2" style="background-color: #0c2ccc !important;">
                        {{ model._id ? "Actualizar" : "Guardar" }}
                      </button>
         </template>
        </Modal>
        <div v-if="ifGrid">
      <GridDistributivo :docentes="listDocentes" :cursos="listniveles" :materias="listMaterias" @myEventClosedAgGrid="closeAgGrid" @getData="refreshData"/>
    </div>
    </div>
</template>
<script src="./Distributivov1.js"></script>

