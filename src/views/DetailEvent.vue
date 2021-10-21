<template>
    <div>
        <div class="row">
            <div class="col-md-7">
                <h5> {{ Event.name }} </h5>
            </div>
            <div class="col-md-5 d-grid">
                <button class="btn btn-primary">Register for this event</button>
            </div>
        </div>
        <div class="row mt-3">
            <div class="col-md-12">
                <TableEvent :EventData="Event"></TableEvent>
            </div>
        </div>
    </div>
</template>
<script>
import axios from 'axios'
import TableEvent from '../components/table-event.vue'
export default {
    name : 'DetailEvent',
    components :{
        TableEvent
    },
    data(){
        return{
            OrganizerSlug : this.$route.params.SlugOrganizer,
            EventSlug : this.$route.params.SlugEvent,
            Event : {}
        }
    },
    mounted(){
        this.DatosEventos();
    },
    methods : {
        DatosEventos(){
            axios.get('organizer/'+this.OrganizerSlug + '/events/' + this.EventSlug)
            .then((response) => {
                if(response.status == 200){
                    this.Event = response.data;
                }
            })
            .catch((error) => {
                console.log(error);
            })
        }
    }
}
   

</script>