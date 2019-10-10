<template>
    <v-container grid-list-xl>
        <v-layout row wrap>

                <!-- CARD TASK TEMPALTE -->
            <v-flex md4>
                <h1 class="text-center">CARDS LIST</h1>
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
                        {{item.name}}
                        </v-chip>
                        <!-- taskDone show -->
                        <span>{{item.taskDone}}</span>
                        <!-- Date picker show -->
                        <div class="font-weight-regular grey--text">
                        <v-icon>mdi-calendar</v-icon>
                        {{item.picker}}</div>
                        <!-- Building Appartment Room show -->
                        <div>
                           <v-icon>mdi-home-modern</v-icon>{{item.Building}} 
                           <v-icon>mdi-home</v-icon>{{item.Appartment}}
                           <v-icon>mdi-home-map-marker</v-icon>{{item.Room}}
                        </div><br>
                        <!-- Action to do show -->
                        <p><strong>Action to do :</strong> {{item.descripcion}}</p>
                        <!-- email show -->
                        <p>
                        <v-icon>mdi-email-outline</v-icon>:
                        {{item.email}}</p>
                        <!-- Phone number show -->
                        <p>
                        <v-icon>mdi-phone</v-icon>   
                        Phone number : {{item.phoneNumber}}</p>

                        <v-btn color="warning" class="mx-3 ml-0"  @click="editarTarea(index)">
                            <v-icon>mdi-nintendo-switch</v-icon>
                            Editar</v-btn>

                        <v-btn color="error" @click="eliminarTarea(item.id)">
                            <v-icon>mdi-delete-circle</v-icon>
                            Eliminar
                        </v-btn>
                    </v-card-text>
                </v-card>
            </v-flex>


                    <!-- FORM -->
            <v-flex md8 v-if="formAgregar">
                <h1 class="text-center">FORM</h1>
                <v-card class="mb-3 pa-3">
                    <v-form @submit.prevent="agregarTarea">
                        <!-- Building SELECT -->
                        <v-select
                        v-model="Building"
                        :items="Buildings"
                        label="Select Build"
                        ></v-select>
                        <!-- Appartment SELECT -->
                        <v-select
                        v-model="Appartment"
                        :items="Appartments"
                        label="Select Appartment"
                        ></v-select>
                        <!-- Room SELECT -->
                        <v-select
                        v-model="Room"
                        :items="Rooms"
                        label="Select Room"
                        ></v-select>
                        <!-- Action to do -->
                        <v-textarea 
                        label="Action to do :" 
                        v-model="descripcion"
                        ></v-textarea>
                        <!-- Task DONE -->
                        <div>Activate if task is done:</div>
                        <v-switch 
                        v-model="taskDone"
                        ></v-switch>
                        
                        <!-- Date PICKER -->
                        <div>
                        Select a day:
                        <v-icon>mdi-calendar-plus</v-icon>
                        </div>
                        <v-row justify="center">
                        <v-date-picker 
                        v-model="picker"
                        full-width=""
                        landscape=""
                        ></v-date-picker>
                        </v-row>
                        <!-- Name of responsable -->
                        <div class="mt-5">
                        Name <v-icon>mdi-account</v-icon>
                        </div>
                        <v-text-field
                        v-model="name"
                        :counter="30"
                        label="Name of responsable"
                        required
                        ></v-text-field>
                        <!-- @Email of responsable -->
                        Email <v-icon>mdi-email</v-icon>
                        <v-text-field
                        v-model="email"
                        label="E-mail"
                        required
                        ></v-text-field>
                        <!-- Phone Number -->
                        Phone<v-icon>mdi-cellphone-basic</v-icon> 
                        <v-text-field
                        v-model="phoneNumber"
                        label="Insert phone number (+33)"
                        type="tel"
                        required
                        >
                        </v-text-field>

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
                        v-model="Building"
                        :items="Buildings"
                        label="Select Build"
                        ></v-select>
                        <!-- Appartment SELECT -->
                        <v-select
                        v-model="Appartment"
                        :items="Appartments"
                        label="Select Appartment"
                        ></v-select>
                        <!-- Room SELECT -->
                        <v-select
                        v-model="Room"
                        :items="Rooms"
                        label="Select Room"
                        ></v-select>
                        <!-- Action to do -->
                        <v-textarea 
                        label="Action to do :" 
                        v-model="descripcion"
                        ></v-textarea>
                        <!-- Task DONE -->
                        <div>Activate if task is done:</div>
                        <v-switch 
                        v-model="taskDone"
                        ></v-switch>
                        
                        <!-- Date PICKER -->
                        <div>
                        Select a day:
                        <v-icon>mdi-calendar-plus</v-icon>
                        </div>
                        <v-row justify="center">
                        <v-date-picker 
                        v-model="picker"
                        full-width=""
                        landscape=""
                        ></v-date-picker>
                        </v-row>
                        <!-- Name of responsable -->
                        <div class="mt-5">
                        Name <v-icon>mdi-account</v-icon>
                        </div>
                        <v-text-field
                        v-model="name"
                        :counter="30"
                        label="Name of responsable"
                        required
                        ></v-text-field>
                        <!-- @Email of responsable -->
                        Email <v-icon>mdi-email</v-icon>
                        <v-text-field
                        v-model="email"
                        label="E-mail"
                        required
                        ></v-text-field>
                        <!-- Phone Number -->
                        Phone<v-icon>mdi-cellphone-basic</v-icon> 
                        <v-text-field
                        v-model="phoneNumber"
                        label="Insert phone number (+33)"
                        type="tel"
                        required
                        >
                        </v-text-field>
                        <v-btn block color="warning" type="submit">Edit task</v-btn>
                    </v-form>
                </v-card>
            </v-flex>


        </v-layout>


                    <!-- SNACKBAR // ALERT-->
                    <v-snackbar
                            v-model="snackbar"

                            >
                            {{ snackbarText }}
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

            tasksList: [],
            Building: '',
            Appartment: '',
            Room: '',
            descripcion: '',
            taskDone: '',
            picker: '',
            name: '',
            email: '',
            phoneNumber: '',


            snackbar: false,
            snackbarText:'',

            formAgregar: true,

            indexTarea: '',



        }
    },
    methods: {
        agregarTarea(){
            console.log(this.Building, this.Appartment, this.Room, this.descripcion, this.taskDone, this.picker,this.titulo,this.email,this.phoneNumber);
            if( this.nombre === '' || 
                this.descripcion === '' || 
                this.Building ===''
                ){
                this.snackbar = true
                this.snackbarText = 'Please insert all fields'
            }else{
                this.tasksList.push({
                    id: Date.now(),
                    Building: this.Building,
                    Appartment: this.Appartment,
                    Room: this.Room,
                    descripcion: this.descripcion,
                    taskDone: this.taskDone,
                    picker: this.picker,
                    name: this.name,
                    email: this.email,
                    phoneNumber: this.phoneNumber


                })
                this.Building = '',
                this.Appartment = '',
                this.Room = '',
                this.descripcion = '',
                this.taskDone = '',
                this.picker = '',
                this.name = '',
                this.email = '',
                this.phoneNumber = '',


                this.snackbar = true
                this.snackbarText = 'Task added correctly'

            }
        },
        eliminarTarea(id){
            this.tasksList = this.tasksList.filter(e => e.id != id)
        },
        editarTarea(index){
            this.formAgregar = false
            this.Building = this.tasksList[index].Building
            this.Appartment = this.tasksList[index].Appartment
            this.Room = this.tasksList[index].Room
            this.descripcion = this.tasksList[index].descripcion
            this.taskDone = this.tasksList[index].taskDone
            this.picker = this.tasksList[index].picker
            this.name = this.tasksList[index].name
            this.email = this.tasksList[index].email
            this.phoneNumber = this.tasksList[index].phoneNumber
            this.indexTarea = index
        },
        saveEdit(){
            this.tasksList[this.indexTarea].Building = this.Building
            this.tasksList[this.indexTarea].Appartment = this.Appartment
            this.tasksList[this.indexTarea].Room = this.Room
            this.tasksList[this.indexTarea].descripcion = this.descripcion
            this.tasksList[this.indexTarea].taskDone = this.taskDone
            this.tasksList[this.indexTarea].picker = this.picker
            this.tasksList[this.indexTarea].name = this.name
            this.tasksList[this.indexTarea].email = this.email
            this.tasksList[this.indexTarea].phoneNumber = this.phoneNumber
            this.formAgregar = true
            this.Building = ''
            this.Appartment = ''
            this.Room = ''
            this.descripcion = ''
            this.taskDone = ''
            this.picker = ''
            this.name = ''
            this.email = ''
            this.phoneNumber = ''

            this.snackbar = true
            this.snackbarText = 'Edit correct'
            
        }
    }
}
</script>