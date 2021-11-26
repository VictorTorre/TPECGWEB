<template>
  <v-data-table
    :headers="headers"
    :items="pacientes"
    :search="search"
    sort-by="nombre"
    class="elevation-1"
    justify="center"
  >
    <template v-slot:top>
      <v-toolbar flat color="white">
        <v-divider class="mx-4" inset vertical />
        <v-spacer></v-spacer>
        <v-text-field
          label="Search User"
          append-icon="search"
          class="text-xs-center"
          v-model="search"
          single-line
          hide-details
        ></v-text-field>
        <v-spacer></v-spacer>
        <v-dialog v-model="dialog" max-width="500px">
          <v-card>
            <v-card-title>
              <span class="headline">{{ formTitle }}</span>
            </v-card-title>

            <v-card-text>
              <v-container>
                <v-row>
                  <v-col cols="12" sm="12" md="12">
                    <v-text-field v-model="id_paciente" label="#"></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="12" md="12">
                    <v-text-field
                      v-model="nombre"
                      label="Nombre"
                    ></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="12" md="12">
                    <v-text-field
                      v-model="apellido"
                      label="Apellido"
                    ></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="12" md="12">
                    <v-text-field
                      type="dni"
                      v-model="birth"
                      label="Dni"
                    ></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="12" md="12">
                    <v-text-field
                      v-model="edad"
                      label="Edad"
                    ></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="12" md="12">
                    <v-text-field v-model="polar_h10" label="Polar_h10"></v-text-field>
                  </v-col>
                </v-row>
              </v-container>
            </v-card-text>
          </v-card>
        </v-dialog>
      </v-toolbar>
    </template>
    <template v-slot:item="{ item }">
      <tr>
        <td>{{ item.id_paciente }}</td>
        <td>{{ item.nombre }}</td>
        <td>{{ item.apellido }}</td>
        <td>{{ item.dni }}</td>
        <td>{{ item.edad }}</td>
        <td>{{ item.polar_h10 }}</td>

        <td class="justify-center layout px-0">
          <v-icon small class="mr-2">description</v-icon>
          <v-icon small class="mr-2">delete</v-icon>
        </td>
      </tr>
    </template>

    <template v-slot:no-data>
      <v-btn color="primary" @click="listPacientes">Reset</v-btn>
    </template>
  </v-data-table>
</template>

<script>
import axios from "axios";
export default {
  data: () => ({
    search: "",
    id_paciente: "",
    nombre: "",
    apellido: "",
    dni: "",
    edad: "",
    polar_h10: "",
    dialog: false,
    pacientes: [],
    headers: [
        { text: "Id_Paciente", value: "id_paciente", sortable: true },
        { text: "Nombre", value: "nombre", sortable: true },
        { text: "Apellido", value: "apellido", sortable: false },
        { text: "Dni", value: "dni", sortable: false },
        { text: "Edad", value: "edad", sortable: false },
        { text: "Polar_h10", value: "polar_h10", sortable: false }
    ],
  }),
  computed: {
  },
  watch: {
    dialog(val) {
      val || this.close();
    },
  },
  created() {
    this.listPacientes();
  },
  methods: {
    listPacientes() {
      let me = this;
      axios
        .get("api/Pacientes")
        .then(function(response) {
          me.pacientes = response.data;
        })
        .catch(function(error) {
          console.log(error);
        });
    },
    close() {
      this.dialog = false;
    },
    clean() {
      this.id = "";
      this.name = "";
      this.lastname = "";
      this.description = "";
      this.birth = "";
      this.address = "";
      this.phone = "";
      this.age = "";
      this.email = "";
      this.country = "";
      this.gender = "";
      this.password = "";
    },
  },
};
</script>