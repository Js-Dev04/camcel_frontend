<template>
  <div class="q-pa-md">
    <q-header elevated style="padding: 0 20px;" class="row justify-between bg-teal-10">
      <div>
        <q-toolbar class="row items-center">
          <q-btn flat @click="drawer = !drawer" round dense icon="menu" />
          <q-toolbar-title>Camcel</q-toolbar-title>
        </q-toolbar>
      </div>
     
      <div class="row">
        <chat/>
        <q-btn flat icon="person">
          <q-menu>
            <q-list style="min-width: 100px">
              <q-item clickable v-close-popup>
                <q-item-section>Perfil</q-item-section>
              </q-item>

              <q-separator />
              <q-item clickable v-close-popup>
                <q-item-section>Empresa</q-item-section>
              </q-item>

              <q-separator />
              <q-item clickable v-close-popup>
                <q-item-section>Documentos</q-item-section>
              </q-item>

              <q-separator />
              <q-item clickable v-close-popup>
                <q-item-section>Descargas</q-item-section>
              </q-item>

              <q-separator />
              <q-item clickable v-close-popup>
                <q-item-section>Configuracion</q-item-section>
              </q-item>

              <q-separator />
              <q-item clickable v-close-popup>
                <q-item-section>Cerrar Sesion</q-item-section>
              </q-item>
            </q-list>
          </q-menu>
        </q-btn>
      </div>
    </q-header>
    
    <q-drawer
      v-model="drawer"
      show-if-above
      :width="200"
      :breakpoint="500"
      bordered
      :class="$q.dark.isActive ? 'bg-grey-9' : 'bg-grey-3'"
    >
    <q-scroll-area
        
        style="
          height: calc(100% - 150px);
          
          
        "
      >
        <q-list padding>
          <q-item clickable v-ripple v-for="(boton , index) in botones"
          :key="index"  @click="pagina(boton.pagina)">
            <q-item-section  avatar>
              <q-icon  :name="boton.icono" />
            </q-item-section>

            <q-item-section > {{ boton.nombre }} </q-item-section>
          </q-item>
        </q-list>
          
      </q-scroll-area>

      
    </q-drawer>

    <q-page-container>
      <q-page class="q-mx-auto" style="max-width: 2000px;">
        <slot/>
      </q-page>
    </q-page-container>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import Chat from 'src/components/Chat.vue' // Ajusta la ruta según la ubicación real de Chat.vue
import { useRouter } from "vue-router"


const router = useRouter()
// Definición de estados reactivos
const text = ref('');
const dialog = ref(false);
const maximizedToggle = ref(true);

const search = ref('');
const botones = ref([
    {nombre:"Empresas",icono:"mdi-office-building-cog-outline",pagina:"/" },
    {nombre:"Documentos",icono:"mdi-file",pagina:"/documentos" },
    {nombre:"His.Trabajo",icono:"mdi-folder-multiple",pagina:"/his.trabajo" },
    {nombre:"Calendario",icono:"mdi-calendar",pagina:"/calendario" },
    {nombre:"Soporte",icono:"mdi-cog-outline",pagina:"/soporte" },
    
  ])
  const pagina =(e)=>{
    router.push(e)
  }
const menuList = [
  {
    icon: 'business_center',
    label: 'Empresas',
    separator: false 
  },
  {
    icon: 'description',
    label: 'Documentos',
    separator: true 
  },
  {
    icon: 'settings',
    label: 'Settings',
    separator: false
  },
  {
    icon: 'logout',
    iconColor: 'primary',
    label: 'Logout',
    separator: false
  }
];

// Definición de `drawer`
const drawer = ref(false);
</script>

