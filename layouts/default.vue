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
                  Bienvenido a ReceFy
                </v-card-title>

                <v-card-subtitle class="text-center mb-3 white--text">
                  <v-icon class="mr-2" color="white">mdi-silverware-fork-knife</v-icon>
                  Cocina con lo que tienes en casa
                </v-card-subtitle>
                <pre>{{ ping }}</pre>
                <v-card-text>
                  <v-form>
                    <v-text-field v-model="formLogin.correo_electronico" dense outlined color="white"
                      label="Correo Electrónico" prepend-inner-icon="mdi-email" class="white-text"></v-text-field>

                    <v-text-field v-model="formLogin.contraseña" dense outlined color="white" label="Contraseña"
                      type="password" prepend-inner-icon="mdi-lock"></v-text-field>
                  </v-form>
                </v-card-text>

                <v-card-actions class="justify-center">
                  <v-btn color="green lighten-1" dark @click="goToRecetas">
                    <v-icon left>mdi-login</v-icon> Iniciar Sesión
                  </v-btn>

                  <v-btn color="blue lighten-1" dark>
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
  name: 'IndexPage',
  data() {
    return {
      formLogin: {
        correo_electronico: '',
        contraseña: '',
      },
      ping: [],
    }
  },

  mounted() {
    this.traerDjango();
  },

  methods: {
    goToRecetas() {
      this.$router.push({ name: 'Recetas' });
    },

    async traerDjango() {
      try {
        const response = await this.$axios.get('jose/');
        console.log('error', response)
        this.ping = response.data;
      } catch (error) {
        console.error({error});
        this.$toast.error(error);

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
