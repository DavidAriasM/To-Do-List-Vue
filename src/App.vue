<template>
  <v-app>
    <v-app-bar app color="purple" dark>
      <div class="d-flex align-center">
        <h1>TodoList</h1>
      </div>
    </v-app-bar>
    <v-main>
      <router-view/>
    </v-main>
    <Footer/>
  </v-app>
</template>

<script>
import Footer from './components/Footer.vue'
import { mapActions } from 'vuex';
export default {
  components:{
    Footer
  },
  name: 'App',

  data: () => ({
    //
  }),
  methods:{
    ...mapActions(['cargarLocalStorage'])
  },
  created(){
    this.cargarLocalStorage()
  }
};
</script>
