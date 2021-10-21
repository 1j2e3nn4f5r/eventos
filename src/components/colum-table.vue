<template>
    <div>
        {{Titulo}}
    </div>
</template>
<script>
export default {
    name : 'ColumTable',
    props : {
        Hora : String,
        Sessiones : Array
    },
    data(){
        return{
            Titulo : ''
        }
    },
    mounted(){
        this.ValidarSesion();
    },
    methods :{
        ValidarSesion(){
            this.Sessiones.forEach(Sesion => {
              let HoraSesion = Sesion.start.substr(11,2);
              
              if(HoraSesion == this.Hora){
                  this.Titulo = Sesion.title;
              }
            });
        }
    }
}
</script>