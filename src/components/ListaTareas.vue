<template>
  <v-simple-table>
    <template v-slot:default>
      <thead>
        <tr>
          <th class="text-center">Tarea</th>
          <th class="text-center">Descripción</th>
          <th class="text-center">Tipo de Tarea</th>
          <th class="text-center">Estado</th>
          <th class="text-center">Editar</th>
          <th class="text-center">Eliminar</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, index) in tareas" :key="index">
          <td :style="item.estado ? 'text-decoration:line-through;' : 'text-decoration:none;'">{{ item.tarea }}</td>
          <td>{{ item.descripcion }}</td>
          <td>{{ item.select }}</td>
          <td><v-chip close-icon="mdi-close-outline" dark :color="item.estado ? 'green' : '' ">{{ item.estado ? 'Realizada' : 'Pendiente' }}</v-chip></td>
          <td><v-btn depressed color="primary" @click="procesarEditarTarea(item)">Editar</v-btn></td>
          <td><v-btn depressed color="error" @click="eliminarTarea(item.id)">Eliminar</v-btn></td>
        </tr>
      </tbody>
      {{ mensajeSinTareas }}
    </template>
  </v-simple-table>
</template>
<script>
import { mapActions, mapState } from 'vuex'
export default {
    computed:{
        ...mapState(['tareas']),
        mensajeSinTareas(){
          if(this.tareas.length === 0){
            return 'Sin tareas registradas'
          }
        }
    },
    methods:{
      ...mapActions(['editarTarea', 'eliminarTarea']),
      procesarEditarTarea: function(tarea){
        tarea.estado = !tarea.estado
        this.editarTarea(tarea)
      }
    }
}
</script>