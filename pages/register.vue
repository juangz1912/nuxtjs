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
      <div class="text-subtitle-1 text-medium-emphasis">Register</div>

      <v-text-field
        v-model="user.fullName"
        label="Full Name"
        required
        placeholder="Enter your full name"
      ></v-text-field>
      <p class="text-red">{{ errors.fullName }}</p>

      <v-text-field
        v-model="user.email"
        label="Email address"
        type="email"
        required
        placeholder="Enter your email"
      ></v-text-field>
      <p class="text-red">{{ errors.email }}</p>

      <v-text-field
        :append-inner-icon="visible ? 'mdi-eye-off' : 'mdi-eye'"
        :type="visible ? 'text' : 'password'"
        v-model="user.password"
        label="Create Password"
        required
        placeholder="Create your password"
      ></v-text-field>
      <p class="text-red">{{ errors.password }}</p>

      <v-card
        class="mb-12"
        color="yellow"
        variant="tonal"
      >
        <v-card-text class="text-medium-emphasis text-caption">
          Fill in the required information to create your account.
        </v-card-text>
      </v-card>

      <v-btn
        block
        class="mb-8"
        color="blue"
        size="large"
        variant="tonal"
        @click="register"
      >
        Register
      </v-btn>

      <v-card-text class="text-center">
        <NuxtLink to="/">
          <a
            class="text-blue text-decoration-none"
            href="#"
            rel="noopener noreferrer"
            target="_blank"
          >
            Already have an account? Log in <v-icon icon="mdi-chevron-right"></v-icon>
          </a>
        </NuxtLink>
      </v-card-text>

      <p class="text-red">{{ errors.general }}</p>
    </v-card>
  </div>
</template>

<script setup>

definePageMeta({
  layout: "blank",
});

import axios from "axios";
import { ref, reactive } from 'vue';

const user = ref({
  fullName: '',
  email: '',
  password: '',
});

const visible = ref(false);

const togglePasswordVisibility = () => {
  visible.value = !visible.value;
};

const errors = reactive({
  fullName: '',
  email: '',
  password: '',
  general: '',
});

const register = async () => {
  errors.fullName = '';
  errors.email = '';
  errors.password = '';
  errors.general = '';

  if (!user.fullName) {
    errors.fullName = 'Full Name is required.';
  }
  if (!user.email) {
    errors.email = 'Email is required.';
  }
  if (!user.password) {
    errors.password = 'Password is required.';
  }

  if (user.fullName && user.email && user.password) {
    try {
      const response = await axios.post('http://localhost:3001/register', {
        fullName: user.fullName,
        email: user.email,
        password: user.password,
      });

      if (response.status === 200) {
        console.log('Registration successful');
        // Redirect the user to the desired page here
      } else {
        errors.general = 'Registration failed';
      }
    } catch (error) {
      console.error('An error occurred:', error);
    }
  }
};
</script>
