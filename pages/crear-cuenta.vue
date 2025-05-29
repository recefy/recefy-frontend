<template>
    <v-app>
        <!-- Fondo con imagen y overlay oscuro -->
        <div class="background">
            <div class="overlay d-flex align-center justify-center fill-height">
                <v-container>
                    <v-row justify="center">
                        <v-col cols="12" md="8" lg="6">
                            <v-card class="glass pa-6" elevation="10">
                                <v-card-title class="justify-center white--text encabezado">
                                    ¡ Crea Tu cuenta Ahora !
                                </v-card-title>

                                <v-card-subtitle class="text-center mt-2 white--text">
                                    <v-icon class="mr-2" color="white">mdi-silverware-fork-knife</v-icon>
                                    Recefy
                                </v-card-subtitle>
                                 <v-divider></v-divider>
                                <v-card-text>
                                    <v-form>
                                        <v-row dense>
                                            <v-col cols="12" sm="12" md="12">
                                                <v-text-field dense outlined v-model="formLoginCrearCuenta.name"
                                                    label="Nombre Usuario"
                                                    prepend-inner-icon="mdi-account-circle"></v-text-field>
                                            </v-col>

                                            <v-col>
                                                <v-text-field v-model="formLoginCrearCuenta.email" dense outlined
                                                    color="white" label="Correo Electrónico"
                                                    prepend-inner-icon="mdi-email" class="white-text"></v-text-field>
                                            </v-col>
                                        </v-row>


                                        <v-text-field v-model="formLoginCrearCuenta.password" dense outlined
                                            color="white" label="Contraseña" type="password"
                                            prepend-inner-icon="mdi-lock"></v-text-field>
                                    </v-form>
                                </v-card-text>

                                <v-card-actions class="justify-center">
                                    <v-btn color="green lighten-1" dark @click="redireccionar()">
                                        <v-icon left>mdi-login</v-icon> Pagina de Inicio
                                    </v-btn>

                                    <v-btn color="blue lighten-1" dark :loading="loading.crear" @click="crearCuenta()">
                                        <v-icon left>mdi-account-plus</v-icon> Crear Cuenta
                                    </v-btn>
                                </v-card-actions>
                            </v-card>
                        </v-col>
                    </v-row>
                </v-container>
            </div>
        </div>
    </v-app>
</template>

<script>
export default {
    data() {
        return {
            loading: {
                crear: false,
            },
            formLoginCrearCuenta: {
                name: '',
                email: '',
                password: '',
            },
            ping: [],
        }
    },



    methods: {
        redireccionar() {
            this.$router.push('/');
        },

        async crearCuenta() {
            try {
                this.loading.crear = true;
                await this.$axios.post('index/crear-cuenta', this.formLoginCrearCuenta)
                this.$toast.success('Cuenta Creada Correctamente')
            } catch (error) {
                this.$toast.error('Ha ocurrido un error al crear la cuenta')
            } finally {
                this.loading.crear = false;
            }
        }
    }
}
</script>

<style scoped>
@import 'typeface-lobster';

.background {
    background-image: url('https://images.pexels.com/photos/842545/pexels-photo-842545.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1');
    background-size: cover;
    background-position: center;
    height: 100vh;
    position: relative;
}

.overlay {
    background: rgba(0, 0, 0, 0.6);
    backdrop-filter: blur(4px);
}

.encabezado {
    font-size: 35px;
    font-family: 'Lobster', cursive;
}

.glass {
    background: rgba(255, 255, 255, 0.1);
    border-radius: 20px;
    backdrop-filter: blur(10px);
    border: 1px solid rgba(255, 255, 255, 0.2);
    color: white;
}
</style>
