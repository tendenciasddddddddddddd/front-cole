<template>
  <nav style="box-shadow: none !important;  "
    class="
      navbar navbar-main navbar-expand-lg
      position-sticky
      top-1
      px-0
      mx-4
      border-radius-xl
      z-index-sticky
      blur
      shadow-blur
      left-auto
      step_7
    "
    id="navbarBlur"
    data-scroll="true"
  >
    <div class="container-fluid py-1 px-1" >
     
     <svg  v-if="!$store.state.isAppMobile" aria-label="Vercel Logo" fill="#000" viewBox="0 0 75 65" width="20"><path d="M37.59.25l36.95 64H.64l36.95-64z"></path></svg>
     <div  v-if="!$store.state.isAppMobile">
        
         <span class="ms-3 s-title-page">
        {{$store.state.first_text}}
        <svg
          xmlns="http://www.w3.org/2000/svg"
          width="1.25em"
          height="1.25em"
          viewBox="0 0 20 20"
          class="small svg-icon fill grey-500 s-mr-2 me-1 ms-1"
          id=""
          fill="currentColor"
          title=""
        >
          <path
            d="M6.52776 18.4722C6.16165 18.1061 6.16165 17.5125 6.52776 17.1464L14.3375 9.33669C14.7036 8.97057 15.2972 8.97057 15.6633 9.33669C16.0294 9.70281 16.0294 10.2964 15.6633 10.6625L7.85359 18.4722C7.48747 18.8383 6.89388 18.8383 6.52776 18.4722Z"
          ></path>
          <path
            d="M6.52776 1.52459C6.16164 1.8907 6.16164 2.4843 6.52776 2.85041L14.3397 10.6624C14.7059 11.0285 15.2995 11.0285 15.6656 10.6624C16.0317 10.2963 16.0317 9.70269 15.6656 9.33657L7.85359 1.52459C7.48747 1.15847 6.89388 1.15847 6.52776 1.52459Z"
          ></path>
        </svg>
       {{$store.state.last_text}}</span
      >


     </div>
      <div
        class="collapse navbar-collapse mt-sm-0 mt-2 me-md-0 me-sm-4"
        id="navbar" 
      >
        <div class="ms-md-auto pe-md-3 d-flex align-items-center">
 
         <svg v-tooltip="'Buscar..'" class="me-3" data-testid="geist-icon" fill="none" height="25" shape-rendering="geometricPrecision" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" viewBox="0 0 24 24" width="25" style="color: #000; cursor: pointer;"><path d="M11 17.25a6.25 6.25 0 110-12.5 6.25 6.25 0 010 12.5z"></path><path d="M16 16l4.5 4.5"></path></svg>
         <svg v-tooltip="'Configuración'" class="me-3" data-testid="geist-icon" fill="none" height="24" shape-rendering="geometricPrecision" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" viewBox="0 0 24 24" width="24" style="color: #000; cursor: pointer;"><circle cx="12" cy="12" r="3"></circle><path d="M19.4 15a1.65 1.65 0 00.33 1.82l.06.06a2 2 0 010 2.83 2 2 0 01-2.83 0l-.06-.06a1.65 1.65 0 00-1.82-.33 1.65 1.65 0 00-1 1.51V21a2 2 0 01-2 2 2 2 0 01-2-2v-.09A1.65 1.65 0 009 19.4a1.65 1.65 0 00-1.82.33l-.06.06a2 2 0 01-2.83 0 2 2 0 010-2.83l.06-.06a1.65 1.65 0 00.33-1.82 1.65 1.65 0 00-1.51-1H3a2 2 0 01-2-2 2 2 0 012-2h.09A1.65 1.65 0 004.6 9a1.65 1.65 0 00-.33-1.82l-.06-.06a2 2 0 010-2.83 2 2 0 012.83 0l.06.06a1.65 1.65 0 001.82.33H9a1.65 1.65 0 001-1.51V3a2 2 0 012-2 2 2 0 012 2v.09a1.65 1.65 0 001 1.51 1.65 1.65 0 001.82-.33l.06-.06a2 2 0 012.83 0 2 2 0 010 2.83l-.06.06a1.65 1.65 0 00-.33 1.82V9a1.65 1.65 0 001.51 1H21a2 2 0 012 2 2 2 0 01-2 2h-.09a1.65 1.65 0 00-1.51 1z"></path></svg>
        <svg v-tooltip="'Notifications'" class="me-3" data-testid="geist-icon" fill="none" height="24" shape-rendering="geometricPrecision" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" viewBox="0 0 24 24" width="24" style="color: #000; cursor: pointer;"><path d="M18 8A6 6 0 006 8c0 7-3 9-3 9h18s-3-2-3-9"></path><path d="M13.73 21a2 2 0 01-3.46 0"></path></svg>
        <svg v-tooltip="'Cerrar sesión'"  @click="logout" data-testid="geist-icon" fill="none" height="24" shape-rendering="geometricPrecision" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" viewBox="0 0 24 24" width="24" style="color: #000; cursor: pointer;"><path d="M15 3h4a2 2 0 012 2v14a2 2 0 01-2 2h-4"></path><path d="M10 17l5-5-5-5"></path><path d="M15 12H3"></path></svg>
        </div>

        <ul class="navbar-nav justify-content-end">
         
          <li class="nav-item dropdown  d-flex align-items-end">
            <a
              href="javascript:;"
              class="nav-link text-body p-0"
            >
              <div class="avatar me-3 ">
                
                <img
                  :src="$store.state.avatar"
                  alt="kal"
                  class="avatar avatar-sm rounded-circle"
                />
              </div>
            </a>

          </li>
          
        </ul>
      </div>
    </div>
  </nav>
</template>

<script>

export default {
  name: "Inicio",
  data() {
    return {
      user: this.$store.state.user,
      foto: '', 
      nombre: '',
      avatar2: 'https://res.cloudinary.com/stebann/image/upload/v1634918496/default-100_namn33.webp',
      isActive: false,
      
    };
  },
  methods: {
    logout() {
      localStorage.clear();
      this.$parent.isLoggedIn = false;
      this.$router.push("/").catch(()=>{});
      //window.location.reload(true);
    },
    inforUsers(){
      const info = JSON.parse(localStorage.getItem('Xf'));
      const avatar = JSON.parse(localStorage.getItem('Avatar'));
      let img= avatar;
      this.$store.commit('agregar2',{img})
      this.nombre= info.nombre;
    },

     isMobile() {
       let estado;
                if( screen.width <= 760 ) {
                  estado = true;
                    this.$store.commit('updatepx',{estado})
                }
                else {
                  estado = false;
                  this.$store.commit('updatepx',{estado})
                }
            },
     
  },
  created() {
    this.inforUsers();
    this.isMobile();
  }
  
};
</script>
