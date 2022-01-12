<template>
    <div class="container">
        <div class="card"> 
            <div class="card-header">
                Editar empleado
            </div>
            <div class="card-body">
                <form v-on:submit.prevent="actualizarRegistro">

                    <div class="form-group">
                      <label for="nombre">Nombre:</label>
                      <input type="text" name="nombre" id="nombre" v-model="empleado.nombre" class="form-control" placeholder="" aria-describedby="helpId">
                      <small id="helpId" class="text-muted">Nombre del empleado</small>
                    </div>

                    <div class="form-group">
                      <label for="correo">Correo:</label>
                      <input type="email" name="correo" id="correo" v-model="empleado.correo" class="form-control" placeholder="" aria-describedby="helpId">
                      <small id="helpId" class="text-muted">Correo del empleado</small>
                    </div>

                    <div class="btn-group" role="group" aria-label="">
                        <button type="submit" class="btn btn-success">Modificar</button>
                        <router-link :to="{name:'Listar'}" class="btn btn-warning">Cancelar</router-link>
                    </div>

                </form>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data() {

        return{
            empleado:{}
        }
    },
    created:function(){
        this.obtenerInformacionID();
    },
    methods:{
        obtenerInformacionID(){
            fetch('http://localhost/empleados/?consultar='+this.$route.params.id)
            .then(respuesta=>respuesta.json())
            .then((datosRespuesta)=>{
                console.log(datosRespuesta)
                this.empleado=datosRespuesta[0];
            })
            .catch(console.log)
        },
        actualizarRegistro(){
            var datosEnviar={id:this.$route.params.id, nombre:this.empleado.nombre, correo:this.empleado.correo}

            fetch('http://localhost/empleados/?actualizar=1'+this.$route.params.id, {
                method:"POST",
                body:JSON.stringify(datosEnviar)
            })
            .then(respuesta=>respuesta.json())
            .then((datosRespuesta=>{
                console.log(datosRespuesta);
                window.location.href='../listar'
            }))

        }
    }

}
</script>