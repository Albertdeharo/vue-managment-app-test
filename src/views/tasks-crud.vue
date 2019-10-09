<template>
    <v-container grid-list-xl>
        <v-layout row wrap>


            <v-flex md6>
                <v-card class="mb-3" v-for="(item, index) in tasksList" :key="index">
                    <v-card-text>
                        <!-- TAG CHIP -->
                            <v-chip
                            class="ma-2"
                            color="pink"
                            label
                            text-color="white"
                            >
                            <v-icon left>mdi-label</v-icon>
                            {{item.titulo}}
                            </v-chip>


                        <p>{{item.descripcion}}</p>
                        <v-btn color="warning" class="mx-3 ml-0">Editar</v-btn>
                        <v-btn color="error" @click="eliminarTarea(item.id)">Eliminar</v-btn>
                    </v-card-text>
                </v-card>
            </v-flex>


            <v-flex md6 >
                <v-card class="mb-3 pa-3">
                    <v-form @submit.prevent="agregarTarea">
                        <v-text-field label="Insert Name" v-model="titulo"></v-text-field>
                        <v-textarea label="description" v-model="descripcion"></v-textarea>
                        <v-btn block color="success" type="submit">Add task</v-btn>
                    </v-form>
                </v-card>
            </v-flex>


        </v-layout>


        <!-- SNACKBAR // ALERT-->
        <v-snackbar
      v-model="snackbar"

    >
      {{ mensaje }}
      <v-btn
        dark
        text
        @click="snackbar = false"
      >
        Close
      </v-btn>
    </v-snackbar>





    </v-container>
</template>

<script>
export default {
    data(){
        return{
            tasksList: [
                {
                    id: 1,
                    titulo: 'Titulo #1',
                    descripcion: 'descripcion 1'
                },
                {
                    id: 2,
                    titulo: 'Titulo #2',
                    descripcion: 'descripcion 2' 
                }
            ],
            titulo: '',
            descripcion: '',
            snackbar: false,
            mensaje:''
        }
    },
    methods: {
        agregarTarea(){
            console.log(this.titulo, this.descripcion);
            if(this.titulo === '' || this.descripcion === ''){
                this.snackbar = true
                this.mensaje = 'llena todos los campos'
            }else{
                this.tasksList.push({
                    id: Date.now(),
                    titulo: this.titulo,
                    descripcion: this.descripcion
                })
                this.titulo = '',
                this.descripcion = ''
                this.snackbar = true
                this.mensaje = 'Tarea agregada'

            }
        },
        eliminarTarea(id){
            this.tasksList = this.tasksList.filter(e => e.id != id)
        }
    }
}
</script>