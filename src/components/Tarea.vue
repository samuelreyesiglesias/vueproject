<template>
    <div>
        <h1 class="display-4 text-center">Listado de Tareas</h1>
        <hr>
        <div class="row">

        <div class="col-lg-8 offset-lg-2">
        <div class="card mt-4">
        <div class="car-body">
            <div class="input-group">
                <input type="text" v-model="tarea"
                class="form-control form-control-lg" placeholder="Agregar tarea" >
                <div class="input-group-append">
                    <button v-on:click="AddItem();"
                    class="btn btn-success btn-lg" >Agregar</button>
                </div>
                
            </div>
        </div>
            <br>
            {{listTareas}}
            <h4 v-if="listTareas.length==0">No hay tareas..</h4>
            <ul class="list-group">
                <li v-for="(tarea,index) of listTareas" :key="index"
                class="list-group-item d-flex justify-content-between">
                    <span class=" cursor" 
                    v-bind:class="{'text-success':tarea.estado}"
                    v-on:click="EditItem(tarea,index);"> 
                        <i v-bind:class="[tarea.estado?'far fa-check-circle':'far fa-circle']"></i>
                    </span> 
                    {{tarea.nombre}}
                    <span class="cursor" v-on:click="DelItem();">
                        <i class="fas fa-trash"></i>
                    </span>
                </li>
            </ul>
            </div>   
        </div>
        </div>
    </div>
</template>

<script>
    export default {
            name: 'Tarea',
            data(){
                return{
                    tarea:'',
                    listTareas:[]
                }
            }, 
            methods:{
                AddItem(){
                    const tarea={
                        nombre:this.tarea,
                        estado:false
                    }
                this.listTareas.push(tarea);
                this.tarea='';
                }, 
                DelItem(index){
                        this.listTareas.splice(index,1);
                },
                EditItem(tarea,index){
                    this.listTareas[index].estado = !tarea.estado;
                }
            }
        }
</script>

<style scoped>
.cursor{
    cursor:pointer
}
</style>