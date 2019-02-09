<template>
  <div id="app" class="container">
    <div class="jumbotron">
      <titulo :titulo="titulo"></titulo>
      <nueva-tarea v-bind:tareas="tareas"></nueva-tarea>
      <lista-tareas :tareas="tareas"></lista-tareas>
    </div>
  </div>
</template>

<script>
import Titulo from "./TituloComponent.vue";
import nuevaTarea from "./nuevaTareaComponent.vue";
import ListaTareas from "./ListaTareasComponent.vue"
export default {
  components: {
    Titulo,
    nuevaTarea,
    ListaTareas
  },

  data() {
    return {
      titulo: "* Lista de tareas Don Pepe*",
      tareas: [],
      nuevaTarea:''
    }
  },
  created(){
    this.$http.get('tareas.json')
    .then(respuesta=>{
     return respuesta.json()
    })
    .then(respuestaJson =>{
      for(let id in respuestaJson){
        let tarea={
          id:id,
          texto:respuestaJson[id].texto,
          terminada:respuestaJson[id].terminada
        }
        this.tareas.push(tarea)
      }
    })
  }

}
</script>

<style lang="scss">
</style>
