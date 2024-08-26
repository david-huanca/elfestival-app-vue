<template>
<div class="min-h-screen flex items-center justify-center bg-base-200">
  <div class="card w-full max-w-lg shadow-xl bg-base-100">
    <div class="card-body">
      <h2 class="card-title text-center">{{ t('register') }}</h2>
      <div class="form-control">
        <label class="label" for="name">
          <span class="label-text">{{ t('name') }}</span>
        </label>
        <input
          type="text"
          id="name"
          v-model="form.name"
          class="input input-bordered"
          :class="{ 'input-error': errors.name }"
          required
        />
        <span v-if="errors.name" class="text-error text-sm">{{ errors.name }}</span>
      </div>

      <div class="form-control">
        <label class="label" for="lastname">
          <span class="label-text">{{ t('lastname') }}</span>
        </label>
        <input
          type="text"
          id="lastname"
          v-model="form.lastname"
          class="input input-bordered"
          :class="{ 'input-error': errors.lastname }"
          required
        />
        <span v-if="errors.lastname" class="text-error text-sm">{{ errors.lastname }}</span>
      </div>

      <div class="form-control">
        <label class="label" for="email">
          <span class="label-text">{{ t('email') }}</span>
        </label>
        <input
          type="email"
          id="email"
          v-model="form.email"
          class="input input-bordered"
          :class="{ 'input-error': errors.email }"
          required
        />
        <span v-if="errors.email" class="text-error text-sm">{{ errors.email }}</span>
      </div>

      <div class="form-control">
        <label class="label" for="phone">
          <span class="label-text">{{ t('phone') }}</span>
        </label>
        <input
          type="tel"
          id="phone"
          v-model="form.phone"
          class="input input-bordered"
          :class="{ 'input-error': errors.phone }"
          required
        />
        <span v-if="errors.phone" class="text-error text-sm">{{ errors.phone }}</span>
      </div>

      <div class="form-control">
        <label class="label" for="country">
          <span class="label-text">{{ t('country') }}</span>
        </label>
        <input
          type="text"
          id="country"
          v-model="form.country"
          class="input input-bordered"
          :class="{ 'input-error': errors.country }"
          required
        />
        <span v-if="errors.country" class="text-error text-sm">{{ errors.country }}</span>
      </div>

      <div class="form-control mt-6">
        <button class="btn btn-primary w-full" @click="submitForm">{{ t('register') }}</button>
      </div>
      
      <div class="mt-4 text-center">
        <label for="theme-toggle" class="label-text mr-2">{{ t('toggleDarkMode') }}</label>
        <input id="theme-toggle" type="checkbox" class="toggle" @click="toggleDarkMode">
      </div>

      <div class="mt-4 text-center">
        <select v-model="language" @change="changeLanguage" class="select select-bordered w-full max-w-xs">
          <option value="en">EN</option>
          <option value="es">ES</option>
          <option value="pt">PT</option>
        </select>
      </div>
    </div>
  </div>
</div>
</template>

<script setup>
import { ref } from 'vue';

const form = ref({
name: '',
lastname: '',
email: '',
phone: '',
country: ''
});

const errors = ref({});
const language = ref('en');

const messages = {
en: {
  register: 'Register',
  name: 'Name',
  lastname: 'Last Name',
  email: 'Email',
  phone: 'Phone',
  country: 'Country',
  toggleDarkMode: 'Toggle Dark Mode',
  required: 'This field is required'
},
es: {
  register: 'Registrarse',
  name: 'Nombre',
  lastname: 'Apellido',
  email: 'Correo Electrónico',
  phone: 'Teléfono',
  country: 'País',
  toggleDarkMode: 'Cambiar Modo Oscuro',
  required: 'Este campo es obligatorio'
},
pt: {
  register: 'Registrar',
  name: 'Nome',
  lastname: 'Sobrenome',
  email: 'Email',
  phone: 'Telefone',
  country: 'País',
  toggleDarkMode: 'Alternar Modo Escuro',
  required: 'Este campo é obrigatório'
}
};

const t = (key) => {
return messages[language.value][key] || key;
};

const toggleDarkMode = () => {
document.documentElement.classList.toggle('dark');
};

const changeLanguage = () => {
// Lógica para cambiar el idioma
};

const submitForm = () => {
errors.value = {};

Object.keys(form.value).forEach((key) => {
  if (!form.value[key]) {
    errors.value[key] = t('required');
  }
});

if (Object.keys(errors.value).length === 0) {
  console.log(form.value);
}
};
</script>
