<template>
  <Head title="About us"/>

  <AuthenticatedLayout>
    <template #header>
      Informacion
    </template>

    <div class="p-4 bg-white rounded-lg shadow-xs">
      Realiza diagramas de forma colaborativa en tiempo real
    </div>
  </AuthenticatedLayout>
</template>

<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import { Head } from '@inertiajs/vue3';
import {onMounted} from 'vue'


</script>
