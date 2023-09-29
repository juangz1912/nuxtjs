<template>
  <div>
    <v-img
      class="mx-auto my-6"
      width="248"
      src="https://upload.wikimedia.org/wikipedia/commons/thumb/a/a7/Koenigsegg_logotype2014.png/1200px-Koenigsegg_logotype2014.png"
    ></v-img>

    <v-card
      class="mx-auto pa-12 pb-8"
      elevation="8"
      max-width="448"
      rounded="lg"
    >
      <div class="text-subtitle-1 text-medium-emphasis">Account</div>

      <!-- Componente de formulario de inicio de sesión -->
      <LoginForm />
      <v-card-text class="text-center">
        <NuxtLink to="/register">
          <a
            class="text-blue text-decoration-none"
            href="#"
            rel="noopener noreferrer"
            target="_blank"
          >
            Sign up now <v-icon icon="mdi-chevron-right"></v-icon>
          </a>
        </NuxtLink>
      </v-card-text>
      
      <v-card
        class="mb-12"
        color="yellow"
        variant="tonal">
        <v-card-text class="text-medium-emphasis text-caption">
          Warning: After 3 consecutive failed login attempts, your account will be temporarily locked for three hours. If you must log in now, you can also click "Forgot login password?" below to reset the login password.
        </v-card-text>
      </v-card>

      <p class="text-red">{{ errors.general }}</p>
    </v-card>
  </div>
</template>

<script>
import LoginForm from '@/components/tasks/LoginForm.vue'; // Importa el componente de formulario de inicio de sesión

definePageMeta({
  layout: "blank",
});

export default {
  components: {
    LoginForm, // Agrega el componente de formulario de inicio de sesión
  },
  data() {
    return {
      errors: {
        general: '',
      },
    };
  },
  methods: {
    login() {
      // Lógica de inicio de sesión aquí
      this.errors.general = ''; // Limpia los errores generales

      // Llama al método de inicio de sesión en el componente LoginForm (puedes personalizar el manejo de errores)
      this.$refs.loginForm.login()
        .catch(error => {
          this.errors.general = 'Invalid email or password. Please try again.'; // Maneja el error de inicio de sesión
        });
    },
  },
};
</script>
