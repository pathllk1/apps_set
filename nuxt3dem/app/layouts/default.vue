<script setup>
import { ref } from 'vue'

const isMobileMenuOpen = ref(false)
const isSidebarCollapsed = ref(true)

const navigation = [
  { label: 'Home', to: '/', icon: 'i-heroicons-home' },
  { label: 'About', to: '/about', icon: 'i-heroicons-information-circle' },
  { label: 'Contact', to: '/contact', icon: 'i-heroicons-envelope' }
]
</script>

<template>
  <UApp class="min-h-screen flex flex-col relative">
    <!-- HEADER -->
    <UHeader 
      class="h-16 sticky top-0 z-50 border-b bg-white/80 dark:bg-gray-900/80 backdrop-blur"
    >
      <template #left>
        <UButton
          icon="i-heroicons-bars-3"
          color="neutral"
          variant="ghost"
          class="mr-2 md:hidden"
          @click="isMobileMenuOpen = true"
        />

        <NuxtLink to="/" class="flex items-center gap-2">
          <AppLogo class="w-auto h-6 shrink-0" />
        </NuxtLink>

        <div class="hidden md:flex items-center gap-4 ml-6">
          <TemplateMenu />
          <nav class="flex items-center space-x-4">
            <NuxtLink 
              v-for="item in navigation" 
              :key="item.to"
              :to="item.to" 
              class="text-sm font-medium hover:text-primary transition-colors"
            >
              {{ item.label }}
            </NuxtLink>
          </nav>
        </div>
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

    <!-- MAIN BODY -->
    <div class="flex flex-1 relative">
      <!-- DESKTOP SIDEBAR -->
      <aside
        :class="[
          'hidden md:flex flex-col fixed top-16 left-0 h-[calc(100vh-4rem-3rem)] border-r bg-white/50 dark:bg-gray-900/50 backdrop-blur transition-all duration-300 z-40',
          isSidebarCollapsed ? 'w-16' : 'w-64'
        ]"
      >
        <div class="flex-1 overflow-y-auto p-3">
          <nav class="flex flex-col space-y-1">
            <NuxtLink 
              v-for="item in navigation" 
              :key="item.to"
              :to="item.to" 
              class="flex items-center gap-3 px-3 py-2 rounded-md hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors group"
              active-class="bg-gray-100 dark:bg-gray-800 text-primary"
            >
              <UIcon :name="item.icon" class="text-xl shrink-0" />
              <span v-if="!isSidebarCollapsed" class="text-sm font-medium truncate">{{ item.label }}</span>
            </NuxtLink>
          </nav>
        </div>

        <!-- COLLAPSE TOGGLE -->
        <div class="p-3 border-t">
          <UButton
            :icon="isSidebarCollapsed ? 'i-heroicons-chevron-double-right' : 'i-heroicons-chevron-double-left'"
            color="neutral"
            variant="ghost"
            block
            @click="isSidebarCollapsed = !isSidebarCollapsed"
          />
        </div>
      </aside>

      <!-- CONTENT AREA -->
      <main
        :class="[
          'flex-1 transition-all duration-300 min-w-0 pb-12',
          isSidebarCollapsed ? 'md:ml-16' : 'md:ml-64'
        ]"
      >
        <UMain class="p-4 md:p-8">
          <slot />
        </UMain>
      </main>
    </div>

    <!-- MOBILE SIDEBAR / MENU -->
    <USlideover v-model:open="isMobileMenuOpen" title="Menu" side="left">
      <template #body>
        <div class="flex flex-col space-y-4 p-4">
          <div class="flex items-center gap-2 pb-4 border-b">
            <AppLogo class="w-auto h-6" />
            <span class="font-bold">Starter</span>
          </div>
          
          <nav class="flex flex-col space-y-2">
            <NuxtLink 
              v-for="item in navigation" 
              :key="item.to"
              :to="item.to" 
              class="flex items-center gap-3 px-4 py-3 rounded-lg hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors"
              active-class="bg-gray-100 dark:bg-gray-800 text-primary font-semibold"
              @click="isMobileMenuOpen = false"
            >
              <UIcon :name="item.icon" class="text-xl" />
              <span>{{ item.label }}</span>
            </NuxtLink>
          </nav>

          <div class="pt-4 border-t">
            <p class="text-xs font-semibold text-gray-400 uppercase tracking-wider mb-2">Templates</p>
            <TemplateMenu />
          </div>
        </div>
      </template>
    </USlideover>

    <!-- FIXED FOOTER -->
    <footer 
      class="fixed bottom-0 left-0 right-0 h-12 border-t bg-white/80 dark:bg-gray-900/80 backdrop-blur z-50 flex items-center px-4 md:px-6"
    >
      <div class="flex flex-1 items-center justify-between">
        <div class="flex items-center gap-4">
          <p class="text-xs text-gray-500 dark:text-gray-400">
            © {{ new Date().getFullYear() }} Nuxt Starter
          </p>
          <USeparator orientation="vertical" class="h-4" />
          <div class="hidden sm:flex items-center gap-3">
            <NuxtLink to="/" class="text-xs hover:text-primary">Privacy</NuxtLink>
            <NuxtLink to="/" class="text-xs hover:text-primary">Terms</NuxtLink>
          </div>
        </div>

        <div class="flex items-center gap-2">
          <UButton
            to="https://github.com/nuxt-ui-templates/starter"
            target="_blank"
            icon="i-simple-icons-github"
            color="neutral"
            variant="ghost"
            size="xs"
          />
        </div>
      </div>
    </footer>
  </UApp>
</template>