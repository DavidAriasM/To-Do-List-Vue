<template>
  <v-form @submit.prevent="procesarForm(tarea)" ref="form" class="my-5">
    <v-text-field v-model="tarea.tarea" :counter="10" :rules="tareaRules" label="Tarea" required></v-text-field>
    <v-text-field v-model="tarea.descripcion" :counter="50" :rules="descripcionRules" label="Descripción de Tarea" required></v-text-field>
    <v-select v-model="tarea.select" :items="items" :rules="[v => !!v || 'Tipo de tarea es requerido']" label="Tipo de Tarea" required ></v-select>
    <v-btn type="submit" :disabled="validarCampos" elevation="2">Agregar Tarea</v-btn>
  </v-form>
</template>
<script>
import { mapActions, mapState } from 'vuex'
  export default {
    data: () => ({
      valid: true,
      tarea: {
        id: '',
        tarea: '',
        descripcion: '',
        select: null,
        estado: false
      },
      tareaRules: [
            v => !!v || 'Nombre de tarea es requerida',
            v => (v && v.length <= 10) || 'El nombre de tarea debe tener como máximo 10 caracteres',
        ],
      descripcionRules: [
            v => !!v || 'Descripción es requerida',
            v => (v && v.length <= 50) || 'El nombre de tarea debe tener como máximo 10 caracteres',
        ],
      items: [
            'Hogar',
            'Trabajo',
            'Pasatiempo',
      ],
    }),
    computed:{
        ...mapState(['tareas']),
        validarCampos: function(){
           if(this.tarea.tarea.trim() !== '' && this.tarea.descripcion !== '' && this.tarea.select !== null){
             return this.valid = false
           }
             return this.valid = true
        }
    },
    methods: {
     ...mapActions(['enviarFormulario']),
     procesarForm: function(tarea){

         this.tarea.id = this.tareas.length + 1

         this.enviarFormulario(tarea)
         this.tarea = {
            id: '',
            tarea: '',
            descripcion: '',
            select: null,
            estado: false
         }
     }
    },
  }
</script>