<template>
  <div>
    <div
      class="d-flex justify-content-around s-bg-white bottom-navigation-bar s-border-top-grey-300 s-row s-nowrap s-fixed s-bottom-0 s-z-fixed s-w-full">

        <router-link v-if="user.roles.includes('Estudiante')"
        class="bottom-navigation-item s-decoration-none text-center s-column s-cross-center s-main-center s-nowrap s-flex-none  s-blue-500 s-color-grey-600 undefined"
        to="/Consultar-nota"> <i class='bx bx-notepad s-iconsm'></i>
        <span class="text s-font-semibold">Notas</span>
      </router-link>
      <router-link v-if="user.roles.includes('Estudiante')"  :class="{'s-actives': $route.name === 'es2'}"
        class="bottom-navigation-item s-decoration-none text-center s-column s-cross-center s-main-center s-nowrap s-flex-none s-color-grey-600 undefined"
        to="/all-lista"> <i class='bx bx-sitemap s-iconsm'></i>
        <span class="text s-font-semibold">Cursos</span>
      </router-link>
      <router-link v-if="user.roles.includes('Estudiante')"  :class="{'s-actives': $route.name === 'es1'}"
        class="bottom-navigation-item s-decoration-none text-center s-column s-cross-center s-main-center s-nowrap s-flex-none s-color-grey-600 undefined"
        to="/my-lista"> <i class='bx bxs-school s-iconsm'></i>
        <span class="text s-font-semibold">Mis cursos</span>
      </router-link>


      <router-link v-if="user.roles.includes('Docente')"  :class="{'s-actives': $route.name === 'd2'||$route.name === 'd4'}"
        class="bottom-navigation-item s-decoration-none text-center s-column s-cross-center s-main-center s-nowrap s-flex-none s-color-grey-600 undefined"
        to="/opciones-curso"> <i class='bx bx-sitemap s-iconsm'></i>
        <span class="text s-font-semibold">Cursos</span>
      </router-link>
      <router-link v-if="user.roles.includes('Docente')"  :class="{'s-actives': $route.name === 'al'}"
        class="bottom-navigation-item s-decoration-none text-center s-column s-cross-center s-main-center s-nowrap s-flex-none s-color-grey-600 undefined"
        to="/aulas-lista"> <i class='bx bxs-school s-iconsm'></i>
        <span class="text s-font-semibold">Aula virtual</span>
      </router-link>
      <router-link v-if="user.roles.includes('Docente')"  :class="{'s-actives': $route.name === 'dr'}"
        class="bottom-navigation-item s-decoration-none text-center s-column s-cross-center s-main-center s-nowrap s-flex-none s-color-grey-600 undefined"
        to="/zoom"> <i class='bx bxs-camera s-iconsm'></i>
        <span class="text s-font-semibold">Zoom</span>
      </router-link>

      <router-link v-if="user.roles.includes('Docente')||user.roles.includes('Estudiante')"
        class="bottom-navigation-item s-decoration-none text-center s-column s-cross-center s-main-center s-nowrap s-flex-none s-color-grey-600 undefined"
        to="/perfil"> <i class='bx bx-group s-iconsm'></i>
        <span class="text s-font-semibold">Perfil</span>
      </router-link>
      
      <router-link
        class="bottom-navigation-item s-decoration-none text-center s-column s-cross-center s-main-center s-nowrap s-flex-none s-color-grey-600 undefined"
        to="/perfil-docen">
        <div class="notification-btn s-relative undefined false">
          <i class='bx bxs-calendar-event s-iconsm'></i>
        </div>
        <span class="text s-font-semibold">Calendario</span>
      </router-link>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      user: this.$store.state.user,
    }
  },
};
</script>

<style>
.bottom-navigation-bar.show {
  transform: none;
}

.s-bottom-0 {
  bottom: 0;
  left: 0;
}

.s-nowrap {
  flex-wrap: nowrap;
}

.s-w-full {
  width: 100%;
}

.s-z-fixed {
  z-index: 9999;
}

.s-fixed {
  position: fixed;
}

.bottom-navigation-bar {
  height: 3.5rem;
  transition: transform .5s;
  padding-bottom: env(safe-area-inset-bottom);
}

.s-bg-white {
  background: white;
}

.s-border-top-grey-300 {
  border-top: 1px solid #ecf0f3;
}
a:hover {
    color: #019df4 !important;
}

.s-decoration-none {
  text-decoration: none !important;
}

.s-nowrap {
  flex-wrap: nowrap;
}

.s-flex-none {
  flex: none;
}

.bottom-navigation-item {
  width: 20%;
  margin-bottom: 0;
}

.s-color-grey-600 {
  color: rgb(94 94 96);
}

.s-cross-center {
  align-items: center;
  align-content: center;
}

.s-main-center {
  justify-content: center;
}

.s-column {
  flex-direction: column;
}

.bottom-navigation-item .text {
  font-size: .625rem;
}

.s-font-semibold {
  font-weight: 700;
}

.s-iconsm {
  display: block;
  font-size: 22px;
  line-height: 12px;
  padding-top: 8px;
}
.s-actives {
  color: #019df4 !important;
}
</style>
