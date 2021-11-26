<template>
    <v-container>
        <v-row align="center" justify="center">
            <v-col cols="12" sm="10">
                <v-row align="center" justify="center">
                    <v-col cols="12" sm="6">
                        <v-card-text class="mt-12">
                            <h2 class="text-center blue--text">CardioApp</h2>
                            <v-row align="center" justify="center">
                                <v-col cols="12" sm="8">
                                    <v-text-field label="Email" outlined dense color="blue" autocomplete="false" class="mt-16"></v-text-field>
                                    <v-text-field label="Password" outlined dense color="blue" autocomplete="false" type="password"></v-text-field>
                                    <v-row>
                                        <v-col cols="12" sm="7">
                                            <v-checkbox label="Remember Me" class="mt-n1" color="blue"></v-checkbox>
                                        </v-col>
                                        <v-col cols="12" sm="5">
                                            <span class="caption blue--text">Forget Password</span>
                                        </v-col>
                                    </v-row>
                                    <v-btn color="blue" router-link to="/pacientes" dark block tile>Login In</v-btn>
                                </v-col>
                            </v-row>
                        </v-card-text>
                    </v-col>
                </v-row>
            </v-col>
        </v-row>
    </v-container>
</template>

<script>

export default {
    data:() => ({
        step: 1
    }),
    props: {
        source: String
    }
}
</script>

<style scoped>
.v-application .rounded-bl-xl {
    border-bottom-left-radius: 300px !important;
}
.v-application .rounded-br-xl {
    border-bottom-right-radius: 300px !important;
}
</style>
