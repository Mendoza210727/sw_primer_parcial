<template>
  <Head title="Dashboard"/>

  <AuthenticatedLayout>
    <template #header>
      <h1 class="text-3xl font-extrabold text-gray-900">Herramienta de dearrolo colaborativo</h1>
    </template>

    <div class="p-6 bg-gray-50 rounded-lg shadow-lg">
      <div class="mb-6">
        <h2 class="text-2xl font-semibold text-gray-800">Bienvenido a tu herramienta colaborativa</h2>
        <p class="text-gray-500 mt-2">En esta aplicación web podrás crear y gestionar diagramas de secuencia UML de manera colaborativa.</p>
      </div>

      <!-- Example section: Add your dynamic content here -->
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
        <div class="bg-white p-6 rounded-lg shadow-md border border-gray-200">
          <h3 class="text-lg font-semibold text-blue-800 mb-2">Diagramas de Secuencia</h3>
          <img aria-hidden="true" class="object-cover w-full h-40 rounded-lg mb-4" src="/images/UML.png" alt="Diagramas de Secuencia"/>
          <p class="text-gray-600">Crea y edita diagramas de secuencia de forma colaborativa con nuestras herramientas interactivas.</p>
        </div>
        <div class="bg-white p-6 rounded-lg shadow-md border border-gray-200">
          <h3 class="text-lg font-semibold text-green-800 mb-2">Salas Colaborativas</h3>
          <img aria-hidden="true" class="object-cover w-full h-40 rounded-lg mb-4" src="/images/salas.jpg" alt="Salas Colaborativas"/>
          <p class="text-gray-600">Participa en salas colaborativas para trabajar en proyectos con tu equipo en tiempo real.</p>
        </div>
        <div class="bg-white p-6 rounded-lg shadow-md border border-gray-200">
          <h3 class="text-lg font-semibold text-yellow-800 mb-2">Exportación de Código</h3>
          <img aria-hidden="true" class="object-cover w-full h-40 rounded-lg mb-4" src="/images/codigo.jpg" alt="Exportación de Código"/>
          <p class="text-gray-600">Exporta tus diagramas a diversos formatos de código para integrarlos en tus proyectos.</p>
        </div>
      </div>
    </div>
  </AuthenticatedLayout>
</template>

<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import { Head } from '@inertiajs/vue3';
import { onMounted } from 'vue';

onMounted(() => {
  // Fetch data or initialize components if needed
});
</script>

<style scoped>
/* Add any additional styles here */
</style>
