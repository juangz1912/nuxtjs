<template>
  <div>
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
  </div>
</template>

<script setup>
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
});

const register = () => {
  // Lógica de registro aquí (sin axios)
};
</script>
