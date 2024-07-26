<!-- <template>
  <aside class="z-20 hidden w-64 overflow-y-auto bg-gradient-to-r from-blue-500 to-blue-700 md:block flex-shrink-0">
    <div class="py-4 text-white">
      <Link class="ml-6 text-lg font-bold" :href="route('dashboard')">
        Entorno Colaborativo
      </Link>

      <ul class="mt-6">
        <li class="relative px-6 py-3">
          <NavLink :href="route('dashboard')" :active="route().current('dashboard')" class="flex items-center text-white hover:bg-blue-600">
            <template #icon>
              <i class="fas fa-tachometer-alt fa-fw"></i>
            </template>
            <span class="ml-4">Dashboard</span>
          </NavLink>
        </li>

        <li class="relative px-6 py-3">
          <NavLink :href="route('projects.index')" :active="route().current('projects.index')" class="flex items-center text-white hover:bg-blue-600">
            <template #icon>
              <i class="fas fa-project-diagram fa-fw"></i>
            </template>
            <span class="ml-4">Proyectos</span>
          </NavLink>
        </li>

        <li class="relative px-6 py-3">
          <NavLink :href="route('users.index')" :active="route().current('users.index')" class="flex items-center text-white hover:bg-blue-600">
            <template #icon>
              <i class="fas fa-users fa-fw"></i>
            </template>
            <span class="ml-4">Usuarios</span>
          </NavLink>
        </li>

        <li class="relative px-6 py-3">
          <NavLink :href="route('about')" :active="route().current('about')" class="flex items-center text-white hover:bg-blue-600">
            <template #icon>
              <i class="fas fa-info-circle fa-fw"></i>
            </template>
            <span class="ml-4">Informacion</span>
          </NavLink>
        </li>
      </ul>
    </div>
  </aside>
</template>
 -->
<script>
import NavLink from '@/Components/NavLink.vue'
import { Link } from '@inertiajs/vue3';
import { ref } from 'vue'

export default {
  components: {
    NavLink,
    Link,
  },

  setup() {
    let showingTwoLevelMenu = ref(false)

    return {
      showingTwoLevelMenu
    }
  },
}
</script>

<style scoped>
/* Asegúrate de incluir los estilos necesarios si los íconos de Font Awesome no se muestran correctamente */
</style>
