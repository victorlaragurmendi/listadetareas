<template>
    <ul class="list-group">
            <li v-for="(tarea, indice) of tareas" :key="tarea.id" class="list-group-item" v-bind:class="{terminada: tarea.terminada}">
                {{tarea.texto}}
                <span class="pull-right">
                        <button type="button" class="btn btn-success btn-xs glyphicon glyphicon-ok" 
                        v-on:click="estado(indice)"></button>
                        <button type="button" class="btn btn-danger btn-xs glyphicon-remove "
                         v-on:click="borrar(indice)"></button>
                </span>
            </li>
        </ul>
</template>

<script>

export default {

    props:['tareas'],
    methods:{
        estado(indice){
         let   terminada=this.tareas[indice].terminada =!this.tareas[indice].terminada;
         let id=this.tareas[indice].id;

         this.$http.patch('tareas/'+id+'.json',{
             terminada:terminada
         }).then(respuesta=> {console.log(respuesta)})
        },
        borrar:function(indice){
            let id=this.tareas[indice].id;
            this.tareas.splice(indice,1);
            this.$http.delete('tareas/'+id+'.json')
            .then(respuesta=> {console.log(respuesta)})
        }
    }
}
</script>
<style >
.terminada{
    color:gray;
    text-decoration:line-through;
}

</style>
