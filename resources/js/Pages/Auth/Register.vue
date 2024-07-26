<template>
  <GuestLayout>
    <Head title="Register" />

    <div class="flex items-center justify-center min-h-screen bg-gradient-to-r from-blue-400 to-blue-600">
      <div class="w-full max-w-sm p-6 bg-white rounded-lg shadow-md">
        <h1 class="mb-6 text-2xl font-bold text-blue-800">Crear una cuenta</h1>

        <form @submit.prevent="submit">
          <div class="mb-4">
            <InputLabel for="name" value="Nombre" class="text-blue-800"/>
            <TextInput id="name" type="text" class="block w-full mt-1 border-gray-300 focus:border-blue-500" v-model="form.name" required autofocus autocomplete="name" />
            <InputError class="mt-2 text-red-500" :message="form.errors.name" />
          </div>

          <div class="mb-4">
            <InputLabel for="email" value="Email" class="text-blue-800"/>
            <TextInput id="email" type="email" class="block w-full mt-1 border-gray-300 focus:border-blue-500" v-model="form.email" required autocomplete="username" />
            <InputError class="mt-2 text-red-500" :message="form.errors.email" />
          </div>

          <div class="mb-4">
            <InputLabel for="password" value="Contraseña" class="text-blue-800"/>
            <TextInput id="password" type="password" class="block w-full mt-1 border-gray-300 focus:border-blue-500" v-model="form.password" required autocomplete="new-password" />
            <InputError class="mt-2 text-red-500" :message="form.errors.password" />
          </div>

          <div class="mb-6">
            <InputLabel for="password_confirmation" value="Confirmar Contraseña" class="text-blue-800"/>
            <TextInput id="password_confirmation" type="password" class="block w-full mt-1 border-gray-300 focus:border-blue-500" v-model="form.password_confirmation" required autocomplete="new-password" />
            <InputError class="mt-2 text-red-500" :message="form.errors.password_confirmation" />
          </div>

          <div class="flex items-center justify-between">
            <Link :href="route('login')" class="text-sm text-blue-600 underline hover:text-blue-800">
              ya esta registrado?
            </Link>

            <PrimaryButton class="bg-blue-600 hover:bg-blue-700 text-white" :class="{ 'opacity-50': form.processing }" :disabled="form.processing">
              Registrar
            </PrimaryButton>
          </div>
        </form>
      </div>
    </div>
  </GuestLayout>
</template>

<script setup>
import GuestLayout from '@/Layouts/GuestLayout.vue';
import InputError from '@/Components/InputError.vue';
import InputLabel from '@/Components/InputLabel.vue';
import PrimaryButton from '@/Components/PrimaryButton.vue';
import TextInput from '@/Components/TextInput.vue';
import { Head, Link, useForm } from '@inertiajs/vue3';

const form = useForm({
  name: '',
  email: '',
  password: '',
  password_confirmation: '',
  terms: false,
});
const submit = () => {
  form.post(route('register'), {
    onFinish: () => form.reset('password', 'password_confirmation'),
  });
};
</script>
