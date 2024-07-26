<template>
  <header class="z-10 py-4 bg-white shadow-md">
    <div class="container flex justify-between items-center px-6 mx-auto h-full text-blue-800">
      <!-- Mobile hamburger -->
      <button @click="$page.props.showingMobileMenu = !$page.props.showingMobileMenu"
        class="p-1 mr-5 -ml-1 rounded-md md:hidden focus:outline-none focus:shadow-outline-purple" aria-label="Menu">
        <svg class="w-6 h-6" aria-hidden="true" fill="currentColor" viewBox="0 0 20 20">
          <path fill-rule="evenodd"
            d="M3 5a1 1 0 011-1h12a1 1 0 110 2H4a1 1 0 01-1-1zM3 10a1 1 0 011-1h12a1 1 0 110 2H4a1 1 0 01-1-1zM3 15a1 1 0 011-1h12a1 1 0 110 2H4a1 1 0 01-1-1z"
            clip-rule="evenodd"></path>
        </svg>
      </button>

      <!-- Main Navigation Menu -->
      <nav class="flex space-x-4">
        <a :href="route('dashboard')" class="flex items-center text-blue-800 hover:text-blue-600">
          <i class="fas fa-tachometer-alt fa-fw mr-2"></i>
          Dashboard
        </a>

        <a :href="route('projects.index')" class="flex items-center text-blue-800 hover:text-blue-600">
          <i class="fas fa-project-diagram fa-fw mr-2"></i>
          Proyectos
        </a>

        <a :href="route('users.index')" class="flex items-center text-blue-800 hover:text-blue-600">
          <i class="fas fa-users fa-fw mr-2"></i>
          Usuarios
        </a>

        <a :href="route('about')" class="flex items-center text-blue-800 hover:text-blue-600">
          <i class="fas fa-info-circle fa-fw mr-2"></i>
          Información
        </a>
      </nav>

      <!-- Dropdown for Notifications -->
      <Dropdown>
        <template #trigger>
          <button class="align-middle rounded-full focus:shadow-outline-purple focus:outline-none mx-4"
            aria-label="Notifications" aria-haspopup="true">
            <i class="fas fa-bell fa-sm fa-fw"></i>
          </button>
        </template>

        <template #content>
          <ul>
            <li v-for="item in notifications" :key="item.id" class="p-2 border-b">
              Invitacion de {{ item.user_name }}<br>
              Proyecto: {{ item.project_name }} <br>
              <div class="flex justify-between mt-2">
                <SecondaryButton @click="respondInvitation(item.id, 2)">Rechazar</SecondaryButton>
                <SecondaryButton @click="respondInvitation(item.id, 1)">Aceptar</SecondaryButton>
              </div>
            </li>
          </ul>
        </template>
      </Dropdown>

      <!-- Dropdown for User Profile -->
      <Dropdown>
        <template #trigger>
          <button class="flex items-center text-blue-800 hover:text-blue-600 rounded-full focus:outline-none" aria-label="Account"
            aria-haspopup="true">
            <span class="mr-2">{{ $page.props.auth.user.name }}</span>
            <i class="fas fa-user-circle fa-lg"></i>
          </button>
        </template>

        <template #content>
          <DropdownLink :href="route('profile.edit')" class="flex items-center">
            <svg class="mr-3 w-4 h-4" aria-hidden="true" fill="none" stroke-linecap="round" stroke-linejoin="round"
              stroke-width="2" viewBox="0 0 24 24" stroke="currentColor">
              <path
                d="M10.325 4.317c.426-1.756 2.924-1.756 3.35 0a1.724 1.724 0 002.573 1.066c1.543-.94 3.31.826 2.37 2.37a1.724 1.724 0 001.065 2.572c1.756.426 1.756 2.924 0 3.35a1.724 1.724 0 00-1.066 2.573c.94 1.543-.826 3.31-2.37 2.37a1.724 1.724 0 00-2.572 1.065c-.426 1.756-2.924 1.756-3.35 0a1.724 1.724 0 00-2.573-1.066c-1.543.94-3.31-.826-2.37-2.37a1.724 1.724 0 00-1.065-2.572c-1.756-.426-1.756-2.924 0-3.35a1.724 1.724 0 001.066-2.573c-.94-1.543.826-3.31 2.37-2.37.996.608 2.296.07 2.572-1.065z">
              </path>
              <path d="M15 12a3 3 0 11-6 0 3 3 0 016 0z"></path>
            </svg>
            Profile
          </DropdownLink>

          <DropdownLink :href="route('logout')" method="post" as="button" class="flex items-center">
            <svg class="mr-3 w-4 h-4" aria-hidden="true" fill="none" stroke-linecap="round" stroke-linejoin="round"
              stroke-width="2" viewBox="0 0 24 24" stroke="currentColor">
              <path d="M11 16l-4-4m0 0l4-4m-4 4h14m-5 4v1a3 3 0 01-3 3H6a3 3 0 01-3-3V7a3 3 0 013-3h7a3 3 0 013 3v1"></path>
            </svg>
            Log Out
          </DropdownLink>
        </template>
      </Dropdown>
    </div>
  </header>
</template>

<script setup>
import Dropdown from '@/Components/Dropdown.vue'
import DropdownLink from '@/Components/DropdownLink.vue'
import { ref, onMounted } from 'vue';
import { usePage } from '@inertiajs/vue3'
import SecondaryButton from '@/Components/SecondaryButton.vue';

const { props } = usePage()
const notifications = ref([])

onMounted(() => {
  fetchInvitations();
})

const fetchInvitations = () => {
  axios.get('/api/users/invitations', { params: { user_id: props.auth.user.id } })
    .then((response) => {
      notifications.value = response.data;
      console.log(notifications.value);
    })
    .catch(error => console.log(error))
}

const respondInvitation = (invitation_id, status) => {
  axios.put(route('api.invitations.update', invitation_id), { status: status })
    .then(response => {
      console.log(response.data);
      notifications.value = [];
      fetchInvitations();
    })
    .catch(error => console.log(error))
}
</script>

<style scoped>
/* Additional styling for better visuals */
nav a {
  text-decoration: none;
  font-weight: 500;
}

nav a:hover {
  border-bottom: 2px solid #3182ce;
}

nav a i {
  color: #3182ce;
}

button {
  background: none;
  border: none;
}

button:focus {
  outline: none;
  box-shadow: none;
}
</style>
