<template>
    <v-container grid-list-xl>
        <v-layout row wrap>

                <!-- CARD TASK TEMPALTE -->
            <v-flex md6>
                <v-card class="mb-3" v-for="(item, index) in tasksList" :key="index">
                    <v-card-text>
                        <!-- TAG CHIP -->    
                        <v-chip
                        class="ma-2"
                        color="cyan"
                        label
                        text-color="white"
                        >
                        <v-icon left>mdi-account-circle-outline</v-icon>
                        John Leider
                        </v-chip>
                        <!-- Building Appartment Room show -->
                        <div>
                            {{item.Building}} - {{item.Appartment}} - {{item.Room}}
                        </div>
                        <!-- Action to do show -->
                        <p>Action to do : {{item.descripcion}}</p>
                        <!-- email show -->
                        <p>{{item.email}}</p>
                        <!-- Phone number show -->
                        <p>{{item.phoneNumber}}</p>
                        <div class="font-weight-regular grey--text">{{item.email}}</div>

                        <v-btn color="warning" class="mx-3 ml-0"  @click="editarTarea(index)">Editar</v-btn>

                        <v-btn color="error" @click="eliminarTarea(item.id)">
                            <v-icon>mdi-delete-circle</v-icon>
                            Eliminar
                        </v-btn>
                    </v-card-text>
                </v-card>
            </v-flex>


                    <!-- FORM -->

            <v-flex md6 v-if="formAgregar">
                <v-card class="mb-3 pa-3">
                    <v-form @submit.prevent="agregarTarea">
                        <!-- Building SELECT -->
                        <v-select
                            v-model="Building"
                            :items="Buildings"
                            :rules="[v => !!v || 'Item is required']"
                            label="Select Build"
                            required
                        ></v-select>
                        <!-- Appartment SELECT -->
                        <v-select
                            v-model="Appartment"
                            :items="Appartments"
                            :rules="[v => !!v || 'Item is required']"
                            label="Select Appartment"
                            required
                        ></v-select>
                        <!-- Room SELECT -->
                        <v-select
                            v-model="Room"
                            :items="Rooms"
                            :rules="[v => !!v || 'Item is required']"
                            label="Select Room"
                            required
                        ></v-select>
                        <!-- Action to do -->
                        <v-textarea label="description" v-model="descripcion"></v-textarea>
                        <!-- Task DONE -->
                        <v-switch v-model="taskDone"></v-switch>
                        <!-- Date PICKER -->
                         <v-row justify="center">
                            <v-date-picker v-model="picker"></v-date-picker>
                         </v-row>
                        <!-- Name of responsable -->
                        <v-text-field
                        v-model="titulo"
                        :counter="30"
                        label="Name of responsable"
                        required
                        ></v-text-field>
                        <!-- @Email of responsable -->
                        <v-text-field
                        v-model="email"
                        label="E-mail"
                        required
                        ></v-text-field>
                        <!-- Phone Number -->
                        <v-text-field
                        v-model="phoneNumber"
                        label="(phone number) +33"
                        type="tel"
                        required
                        ></v-text-field>

                        <v-btn block color="success" type="submit">Add task</v-btn>
                    </v-form>
                </v-card>
            </v-flex>

                    <!-- FORM EDIT VIEW -->
            <v-flex md6 >
                <v-card class="mb-3 pa-3" v-if="!formAgregar">
                    <v-form @submit.prevent="saveEdit">
                        <!-- Building SELECT -->
                        <v-select
                            v-model="select"
                            :items="items"
                            :rules="[v => !!v || 'Item is required']"
                            label="Item"
                            required
                        ></v-select>
                        <!-- Appartment SELECT -->
                        <v-select
                            v-model="select"
                            :items="items"
                            :rules="[v => !!v || 'Item is required']"
                            label="Item"
                            required
                        ></v-select>


                        <v-text-field label="Insert Name" v-model="titulo"></v-text-field>
                        <v-textarea label="description" v-model="descripcion"></v-textarea>
                        <v-btn block color="warning" type="submit">Edit task</v-btn>
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
            Buildings: [
            'Building 1',
            'Building 2',
            'Building 3',
            'Building 4',
                ],
            Appartments: [
            'Appartment 1',
            'Appartment 2',
                ],
            Rooms:[
            'Room 1',
            'Room 2',
            'Room 3',
                ],

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
            Building: '',
            Appartment: '',
            Room: '',
            descripcion: '',
            taskDone: '',
            picker: '',
            titulo: '',
            email: '',
            phoneNumber: '',


            snackbar: false,
            mensaje:'',

            formAgregar: true,

            indexTarea: '',



        }
    },
    methods: {
        agregarTarea(){
            console.log(this.Building, this.Appartment, this.Room, this.descripcion, this.taskDone, this.picker,this.titulo,this.email,this.phoneNumber);
            if(this.titulo === '' || this.descripcion === ''){
                this.snackbar = true
                this.mensaje = 'llena todos los campos'
            }else{
                this.tasksList.push({
                    id: Date.now(),
                    Building: this.Building,
                    Appartment: this.Appartment,
                    Room: this.Room,
                    descripcion: this.descripcion,
                    taskDone: this.taskDone,
                    picker: this.picker,
                    titulo: this.titulo,
                    email: this.email,
                    phoneNumber: this.phoneNumber


                })
                this.titulo = '',
                this.descripcion = ''


                this.snackbar = true
                this.mensaje = 'Tarea agregada'

            }
        },
        eliminarTarea(id){
            this.tasksList = this.tasksList.filter(e => e.id != id)
        },
        editarTarea(index){
            this.formAgregar = false
            this.titulo = this.tasksList[index].titulo
            this.descripcion = this.tasksList[index].descripcion
            this.indexTarea = index
        },
        saveEdit(){
            this.tasksList[this.indexTarea].titulo = this.titulo
            this.tasksList[this.indexTarea].descripcion = this.descripcion
            this.formAgregar = true
            this.titulo = ''
            this.descripcion = ''
            this.mensaje = 'Edit correct'
            
        }
    }
}
</script>