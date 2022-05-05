<template>
    <v-container>
        <v-row class="text-center">
            <v-col cols="12">
                <h1>TodoList</h1>
                <Form />
                <ListaTareas />
            </v-col>   
        </v-row> 
    </v-container>
</template>
<script>
import Form from '../components/Form'
import ListaTareas from '../components/ListaTareas'
export default {
    components:{Form, ListaTareas},
    data() {
        return {}
    },
    
}
</script>