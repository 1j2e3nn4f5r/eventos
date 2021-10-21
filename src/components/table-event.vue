<template>
    <div>
      <div class="table-responsive">
        <table class="table table-hover table-borderless">
        <thead>
          <th style="width: 15%"></th>
          <th style="width: 10%"></th>
          <th v-for="(Hora, index) in TableThead" :key="index">{{Hora}}</th>
        </thead>
          <tbody v-for="(channel, index) in EventData.channels" :key="index">
          <tr v-for="(room, indexRoom) in channel.rooms" :key="indexRoom">
            <td v-if="indexRoom == 0" :rowspan="channel.rooms.length">
              {{ channel.name }}
            </td>
            <td class="border-start border-end">
              {{room.name}}
            </td>
            <td v-for="(Hora, indexHora) in TableThead" :key="indexHora">
              <ColumTable :Hora="Hora" :Sessiones="room.sessions"></ColumTable>
            </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
</template>
<script>
import axios from 'axios'
import ColumTable from './colum-table.vue'
export default {
    name : 'table-event',
    components : {
      ColumTable
    },
    data(){
      return{
        OrganizerSlug : this.$route.params.SlugOrganizer,
        EventSlug : this.$route.params.SlugEvent,
        EventData : {},
        TableThead : []
      }
    },
    mounted(){
      this.DatosEventos()
    },
    methods :{
      DatosEventos(){
            axios.get('organizer/'+this.OrganizerSlug + '/events/' + this.EventSlug)
            .then((response) => {
                if(response.status == 200){
                    this.EventData = response.data;
                    this.HorasEvento();
                }
            })
            .catch((error) => {
                console.log(error);
            })
        },
      HorasEvento(){
        this.EventData.channels.forEach(Channel => {
          Channel.rooms.forEach(Room => {
            Room.sessions.forEach(Session => {
              let Hora = Session.start.substr(11,2);

              if(!this.TableThead.includes(Hora)){
                this.TableThead.push(Hora);
              }
            })
          })
        })
        this.TableThead = this.TableThead.sort((a,b)=>a-b);
      }
    }
}
</script>