<template>
  <form @submit.prevent="login">
    <v-text-field
      v-model="user.email"
      label="Email"
      required
      type="email"
      placeholder="Enter your email"
    ></v-text-field>

    <v-text-field
      v-model="user.password"
      label="Password"
      required
      type="password"
      placeholder="Enter your password"
    ></v-text-field>

    <v-btn type="submit" block
        class="mb-8"
        color="blue"
        size="large"
        variant="tonal">
      Log In
    </v-btn>
  </form>
</template>

<script setup>
import axios from "axios";

const user = ref({
  email: '',
  password: '',
});

const login = async () => {
  // Validación básica: Verifica si los campos de correo y contraseña están completos
  if (!user.email || !user.password) {
    // Muestra un mensaje de error o maneja la validación según tus necesidades
    console.error('Email and password are required.');
    return;
  }

  try {
    // Envía los datos de inicio de sesión al servidor para verificar la autenticación
    const response = await axios.post('http://localhost:3001/login', {
      email: user.email,
      password: user.password,
    });

    // Si la respuesta es exitosa, redirige al usuario a la página de destino
    if (response.status === 200) {
      console.log('Login successful');
      // Aquí puedes redirigir al usuario a la página deseada, por ejemplo:
      // this.$router.push('/dashboard');
    } else {
      // Maneja el caso en el que la autenticación falla
      console.error('Invalid credentials');
    }
  } catch (error) {
    // Maneja cualquier error de red o de servidor aquí
    console.error('An error occurred:', error);
  }
};
</script>
