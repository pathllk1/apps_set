<script setup>
import { ref } from 'vue'

const open = ref(false)

// ✅ FIX: ADD THIS
const collapsed = ref(true)
</script>

<template>
  <UApp class="min-h-screen flex flex-col">

    <!-- HEADER -->
    <UHeader class="h-16">
      <template #left>
        <UButton
          icon="i-heroicons-bars-3"
          color="neutral"
          variant="ghost"
          class="mr-2 md:hidden"
          @click="open = true"
        />

        <NuxtLink to="/">
          <AppLogo class="w-auto h-6 shrink-0" />
        </NuxtLink>

        <TemplateMenu />

        <nav class="hidden md:flex items-center space-x-4 ml-6">
          <NuxtLink to="/" class="text-sm font-medium">Home</NuxtLink>
          <NuxtLink to="/about" class="text-sm font-medium">About</NuxtLink>
          <NuxtLink to="/contact" class="text-sm font-medium">Contact</NuxtLink>
        </nav>
      </template>

      <template #right>
        <UColorModeButton />
        <UButton
          to="https://github.com/nuxt-ui-templates/starter"
          target="_blank"
          icon="i-simple-icons-github"
          color="neutral"
          variant="ghost"
        />
      </template>
    </UHeader>



    <!-- MAIN -->
    <div class="flex flex-1">

      <!-- ✅ SIDEBAR -->
      <aside
        :class="[
          'hidden md:flex fixed top-16 left-0 h-[calc(100vh-4rem)] border-r p-4 flex-col bg-white dark:bg-gray-900 transition-all duration-300',
          collapsed ? 'w-20' : 'w-64'
        ]"
      >

        <!-- TOGGLE BUTTON -->
        <button
          @click="collapsed = !collapsed"
          class="absolute -right-3 top-1/2 -translate-y-1/2 bg-white dark:bg-gray-800 border rounded-full p-1 shadow"
        >
          <UIcon
            name="i-heroicons-chevron-right"
            :class="[
              'transition-transform duration-300',
              collapsed ? '' : 'rotate-180'
            ]"
          />
        </button>

        <h2 v-if="!collapsed" class="text-lg font-semibold mb-4">Menu</h2>

        <nav class="flex flex-col space-y-2">

          <NuxtLink to="/" class="flex items-center gap-2 px-2 py-2 rounded hover:bg-gray-100 dark:hover:bg-gray-800">
            <UIcon name="i-heroicons-home" class="text-lg" />
            <span v-if="!collapsed">Dashboard</span>
          </NuxtLink>

          <NuxtLink to="/about" class="flex items-center gap-2 px-2 py-2 rounded hover:bg-gray-100 dark:hover:bg-gray-800">
            <UIcon name="i-heroicons-information-circle" class="text-lg" />
            <span v-if="!collapsed">About</span>
          </NuxtLink>

          <NuxtLink to="/contact" class="flex items-center gap-2 px-2 py-2 rounded hover:bg-gray-100 dark:hover:bg-gray-800">
            <UIcon name="i-heroicons-envelope" class="text-lg" />
            <span v-if="!collapsed">Contact</span>
          </NuxtLink>

        </nav>
      </aside>

      <!-- ✅ CONTENT -->
      <UMain
        :class="[
          'flex-1 p-6 transition-all duration-300',
          collapsed ? 'md:ml-20' : 'md:ml-64'
        ]"
      >
        <slot />
      </UMain>

    </div>

    <!-- FOOTER -->
    <USeparator icon="i-simple-icons-nuxtdotjs" />

    <UFooter>
      <template #left>
        <p class="text-sm text-gray-500 dark:text-gray-400">
          Built with Nuxt UI • © {{ new Date().getFullYear() }}
        </p>
      </template>

      <template #right>
        <UButton
          to="https://github.com/nuxt-ui-templates/starter"
          target="_blank"
          icon="i-simple-icons-github"
          color="neutral"
          variant="ghost"
        />
      </template>
    </UFooter>

  </UApp>
</template>