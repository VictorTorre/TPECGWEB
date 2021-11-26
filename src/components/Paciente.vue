<template>
    <div>
        <v-toolbar flat color="white">
            <v-divider
                class="mx-2"
                inset
                vertical
            ></v-divider>
            <v-spacer></v-spacer>
            <v-text-field label="Search Paciente" append-icon="search" class="text-xs-center" v-model="search" single-line hide-details></v-text-field>
            <v-spacer></v-spacer>
            <v-dialog v-model="dialog" max-width="500px">
                <v-card>
                <v-card-title>
                    <span class="headline">{{ formTitle }}</span>
                </v-card-title>

                <v-card-text>
                    <v-container grid-list-md>
                    <v-layout wrap>
                        <v-flex xs12 sm6 md4>
                        <v-text-field v-model="id_paciente" label="Id Paciente"></v-text-field>
                        </v-flex>
                        <v-flex xs12 sm6 md4>
                        <v-text-field v-model="nombre" label="Nombre"></v-text-field>
                        </v-flex>
                        <v-flex xs12 sm6 md4>
                        <v-text-field v-model="apellido" label="Apellido"></v-text-field>
                        </v-flex>
                        <v-flex xs12 sm6 md4>
                        <v-text-field v-model="dni" label="Dni"></v-text-field>
                        </v-flex>
                        <v-flex xs12 sm6 md4>
                        <v-text-field v-model="edad" label="Edad"></v-text-field>
                        </v-flex>
                        <v-flex xs12 sm6 md4>
                        <v-text-field v-model="polar_h10" label="Polar h10"></v-text-field>
                        </v-flex>
                    </v-layout>
                    </v-container>
                </v-card-text>

                <v-card-actions>
                    <v-spacer></v-spacer>
                    <v-btn color="blue darken-1" flat @click="close">Cancel</v-btn>
                    <v-btn color="blue darken-1" flat @click="save">Save</v-btn>
                </v-card-actions>
                </v-card>
            </v-dialog>
        </v-toolbar>
        
        <v-data-table
        :headers="headers"
        :items="atencions"
        class="elevation-1"
        >
        
        <template v-slot:items="props">
            <td>{{ props.item.name }}</td>
            <td class="text-xs-right">{{ props.item.id_paciente }}</td>
            <td class="text-xs-right">{{ props.item.nombre }}</td>
            <td class="text-xs-right">{{ props.item.apellido }}</td>
            <td class="text-xs-right">{{ props.item.dni }}</td>
            <td class="text-xs-right">{{ props.item.edad }}</td>
            <td class="text-xs-right">{{ props.item.polar_h10 }}</td>
            <td class="justify-center layout px-0">
                <v-icon
                    small
                    class="mr-2"
                    @click="editItem(props.item)"
                >
                    edit
                </v-icon>
                <v-icon
                    small
                    @click="deleteItem(props.item)"
                >
                    delete
                </v-icon>
            </td>
        </template>
        <template v-slot:no-data>
            <v-btn color="primary" @click="listPacientes">Reset</v-btn>
        </template>
        </v-data-table>
    </div>
</template>

<script>
    import axios from 'axios'
    
    export default {
        data:() => ({
            search: '',
            id_paciente: '',
            nombre: '',
            apellido: '',
            dni: '',
            edad: '',
            polar_h10: '',
            dialog: false,
            atencions: [],
            valid: 0,
            validMessage: [],
            headers: [
                { text: 'Id_Paciente', value: 'Id_persona', sortable: true },
                { text: 'Nombre', value: 'nombre', sortable: false },
                { text: 'Apellido', value: 'apellido', sortable: false },
                { text: 'Dni', value: 'dni', sortable: false },
                { text: 'Edad', value: 'edad', sortable: false },
                { text: 'Polar_h10', value: 'polar_h10', sortable: false },
            ]
        }),
        computed: {
            formTitle() {
                return'New Paciente';
            }
        },
        watch: {
            dialog (val) {
                val || this.close()
            }
        },
        created() {
            this.listPacientes();
        },
        methods: {
            listPacientes() {
                let me= this;
                axios.get('pacientes').then(function(response){
                    me.pacientes = response.data;
                }).catch(function(error){
                    console.log(error);
                })
            },
            close() {
                this.dialog = false;
            },
            clean() {
                this.id_paciente = "",
                this.nombre = "",
                this.apellido = "",
                this.dni = "",
                this.edad = "",
                this.polar_h10 = ""
            },
            save() {
                let me=this;
                axios.post('pacientes', {
                    'id_paciente' : me.id_paciente,
                    'nombre': me.nombre,
                    'apellido': me.apellido,
                    'dni': me.dni,
                    'edad': me.edad,
                    'polar_h10': me.polar_h10
                }).then(function(response){
                    me.close();
                    me.listPacientes();
                    me.clean();
                }).catch(function(error) {
                    console.log(error);
                });
            }
        }
    }
</script>