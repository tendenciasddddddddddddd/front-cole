<template>
  <div >
    <vue-progress-bar  style="margin-top:-23px"></vue-progress-bar>
      <ProgressBar v-if="isData"></ProgressBar>
      <div v-else >
        <ActionRowHeader :FirstText="'Gestión'" :LastText="' Aulas virtuales'" :numPages="numPages"  :page="page" :IfAdd="1" @pagechanged="onPageChange" @changeSearch="changeSearch" @openCreateCourse="openChildNew"></ActionRowHeader>
        <section class="projects_projects__f_nDO mt-3" v-if="displayedArticles.length" >
            <div v-for="(item, index) in displayedArticles" :key="item.id" class="styles_projectCardWrapper__zSMNk s-mopa animate__animated animate__fadeInUp" :class="[`animations-${index}`]">
                         <a href="javascript:;" @click="openModules(item._id)" class="link_link__LTNaQ styles_projectCard__2QnBU "  >
               <div class="styles_projectCardDetails__vcWBi stack_stack__A16oG">
                 <div class="stack_stack__A16oG">
                   <div class=" d-flex justify-content-start">
                      <span  class="avatar_avatar__OLijw stack_stack__A16oG" v-bind:style="{'background':colorsh[index]}">
                        <span class="in-avatar text-center">
                          
                           <b >{{item.materia.slice(0,2).toUpperCase()}}</b>
                         <!-- <svg data-testid="geist-icon" fill="none" height="24" shape-rendering="geometricPrecision" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" viewBox="0 0 24 24" width="24" style="color: white"><path d="M8 3v3a2 2 0 01-2 2H3m18 0h-3a2 2 0 01-2-2V3m0 18v-3a2 2 0 012-2h3M3 16h3a2 2 0 012 2v3"></path></svg> -->
                        </span>
                      </span>
                      <div class="stack_stack__A16oG ms-3">
                        <span class="cardTitle fuente"  style="font-size: 16px;margin-top: -5px;">{{item.materia}}</span>
                          <span class="tag fuente tag-purple">{{item.icono}}</span>
                      </div>
                   </div>
                   <div>
                     <p class="cardTitle fuente mt-2" style="font-size: .80rem;"> {{item.nombre}}</p>
                   </div>
                   <div>
                     <span class="text-xs  fuente mt-2" style="color: #516f90 !important;">
                   {{item.fecha}}
                </span>
                <span style="color:black">
                 <svg viewBox="0 0 24 24" width="15" height="15" stroke="currentColor" stroke-width="2" fill="none" stroke-linecap="round" stroke-linejoin="round" class="css-i6dzq1"><circle cx="18" cy="18" r="3"></circle><circle cx="6" cy="6" r="3"></circle><path d="M13 6h3a2 2 0 0 1 2 2v7"></path><line x1="6" y1="9" x2="6" y2="21"></line></svg>
                </span>
                   </div>
                 </div>
               </div>
             </a>
             <a href="javascript:;"  @click="openModules(item._id)" class="styles_visitButton__Nc7Vp ">
               <span class="s-btn-redondo">
                   <svg viewBox="0 0 24 24" width="18" height="18" stroke="currentColor" stroke-width="2" fill="none" stroke-linecap="round" stroke-linejoin="round" class="css-i6dzq1"><path d="M18 13v6a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h6"></path><polyline points="15 3 21 3 21 9"></polyline><line x1="10" y1="14" x2="21" y2="3"></line></svg>
               </span>
             </a>
           </div>
        </section>
         <section v-else>
          <NoFound />
        </section>
      </div>
    <div v-if="ifChildGroup">
      <ListAllEstudiantes :idGet="key" @myEvent="closedChildGruopen"></ListAllEstudiantes>
    </div>
    <div v-if="ifChildNew">
      <CreateCurso @myEvent2="closedChildNew" @clickSave="refresh"></CreateCurso>
    </div>
  </div>
</template>
<script src="./AulasListas.js"></script>