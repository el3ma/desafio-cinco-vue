<template>
  <div id="app" class="container">
    <div class="row container d-flex justify-content-between">
      <div class="col-3" v-if="usuarios.length">
        <CardUsuario 
        :imagenUsuario="usuarios[0].picture.large" 
        :nombre="`${usuarios[0].name.first} ${usuarios[0].name.last}`"
        alineacion="left"
        @enviarChat="agregarMensaje"/>
      </div>
      <div class="col-6">
        <CardChat
        :mensajes="mensajes" />
      </div>
      <div class="col-3" v-if="usuarios.length">
        <CardUsuario 
        :imagenUsuario="usuarios[1].picture.large" 
        :nombre="`${usuarios[1].name.first} ${usuarios[1].name.last}`"
        alineacion="right"
        @enviarChat="agregarMensaje" />
      </div>
    </div>





  </div>
</template>

<script>
import axios from 'axios';
import CardUsuario from './components/CardUsuario.vue';
import CardChat from './components/CardChat.vue';


export default {
  name: 'App',
  components: {
    CardUsuario,
    CardChat
  },
  data() {
    return {
      usuarios: [],
      mensajes:[]
    }
  },
  methods:{
    agregarMensaje: function(nuevoMensaje){
      this.mensajes.push(nuevoMensaje)
      console.log(this.mensajes)
    }
  },
  async mounted() {
    try {
      let response = await axios.get("https://randomuser.me/api/?results=2");
      let { data } = response;
      this.usuarios = data.results;
    } catch (error) {
      console.log(error);
      if (error.code == "ERR_NETWORK") {
        return alert("En estos momento el servidor está caído, puede intentar más tarde.")
      }
      if (error.response.status == 404) {
        alert("El recurso que está buscando no existe.");
      } else {
        alert("El servidor en estos momentos no puede procesar su solicitud.")
      }
    }
  },
  
}
</script>

<style>
#app{
  display: flex;
  margin: 10% 20%;
}
</style>
