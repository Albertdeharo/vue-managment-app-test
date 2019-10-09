<template>
    <v-container grid-list-xl>
        <v-layout row wrap>


            <v-flex md6>
                <v-card class="mb-3">
                    <v-card-text>
                        <!-- TAG CHIP -->
                            <v-chip
                            class="ma-2"
                            color="pink"
                            label
                            text-color="white"
                            >
                            <v-icon left>mdi-label</v-icon>
                            Name task to do #1
                            </v-chip>


                        <p>Lorem ipsum dolor sit amet consectetur, adipisicing elit. In, exercitationem laboriosam. Quia voluptatibus excepturi fugiat maiores ex, incidunt, dolores velit esse assumenda officia adipisci libero harum tempore corporis fuga! Soluta!</p>
                        <v-btn color="warning" class="mx-3 ml-0">Editar</v-btn>
                        <v-btn color="error">Eliminar</v-btn>
                    </v-card-text>
                </v-card>
            </v-flex>


            <v-flex md6 class="mb-3">
                <v-card>
                    ffdfd
                </v-card>
            </v-flex>


        </v-layout>
    </v-container>
</template>

<script>
export default {
    data(){
        return{
            tasksList
        }
    }
}
</script>