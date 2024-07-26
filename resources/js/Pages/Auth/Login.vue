<template>
  <GuestLayout>
    <Head title="Log in"/>

    <div class="flex items-center justify-center min-h-screen bg-gradient-to-r from-blue-400 to-blue-600">
      <div class="w-full max-w-sm p-6 bg-white rounded-lg shadow-md">
        <h1 class="text-2xl font-bold text-blue-800 mb-6">Iniciar sesión</h1>

        <div v-if="status" class="mb-4 text-sm font-medium text-blue-600">
          {{ status }}
        </div>

        <form @submit.prevent="submit">
          <div class="mb-4">
            <InputLabel for="email" value="Email" class="text-blue-800"/>
            <TextInput id="email" type="email" class="block w-full mt-1 border-gray-300 focus:border-blue-500" v-model="form.email" required autofocus autocomplete="username" />
            <InputError class="mt-2 text-red-500" :message="form.errors.email" />
          </div>

          <div class="mb-6">
            <InputLabel for="password" value="Contraseña" class="text-blue-800"/>
            <TextInput id="password" type="password" class="block w-full mt-1 border-gray-300 focus:border-blue-500" v-model="form.password" required autocomplete="current-password"/>
            <InputError class="mt-2 text-red-500" :message="form.errors.password" />
          </div>

          <div class="flex items-center mb-6">
            <Checkbox name="remember" v-model:checked="form.remember"/>
            <span class="ml-2 text-sm text-blue-800">Recordar contraseña</span>
          </div>

          <div class="flex items-center justify-between">
            <Link v-if="canResetPassword" :href="route('password.request')" class="text-sm text-blue-600 hover:text-blue-800">
              Olvidaste tu contraseña?
            </Link>

            <PrimaryButton class="bg-blue-600 hover:bg-blue-700 text-white" :class="{ 'opacity-50': form.processing }" :disabled="form.processing">
              Iniciar
            </PrimaryButton>
          </div>
        </form>
      </div>
    </div>

  </GuestLayout>
</template>

<script setup>
import Checkbox from '@/Components/Checkbox.vue';
import GuestLayout from '@/Layouts/GuestLayout.vue';
import InputError from '@/Components/InputError.vue';
import InputLabel from '@/Components/InputLabel.vue';
import PrimaryButton from '@/Components/PrimaryButton.vue';
import TextInput from '@/Components/TextInput.vue';
import { Head, Link, useForm } from '@inertiajs/vue3';
defineProps({
    canResetPassword: Boolean,
    status: String,
});
const form = useForm({
    email: '',
    password: '',
    remember: false
});
const submit = () => {
    form.post(route('login'), {
        onFinish: () => form.reset('password'),
    });
};
</script>
