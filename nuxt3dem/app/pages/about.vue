<script setup>
const values = [
  {
    title: 'Innovation',
    description: 'We push boundaries and explore new technologies to deliver cutting-edge solutions.',
    icon: 'i-heroicons-light-bulb'
  },
  {
    title: 'User-Centric',
    description: 'Our users are at the heart of everything we do, ensuring accessibility and ease of use.',
    icon: 'i-heroicons-user-group'
  },
  {
    title: 'Excellence',
    description: 'We strive for the highest quality in every line of code and design pixel.',
    icon: 'i-heroicons-star'
  },
  {
    title: 'Collaboration',
    description: 'We believe in the power of teamwork and open-source contribution.',
    icon: 'i-heroicons-chat-bubble-left-right'
  }
]

const team = [
  {
    name: 'Alex Rivera',
    role: 'Lead Architect',
    avatar: 'https://i.pravatar.cc/150?u=alex',
    bio: 'Passionate about building scalable Nuxt applications.'
  },
  {
    name: 'Sarah Chen',
    role: 'UI/UX Designer',
    avatar: 'https://i.pravatar.cc/150?u=sarah',
    bio: 'Creating beautiful and intuitive user experiences.'
  },
  {
    name: 'Jordan Smith',
    role: 'Frontend Engineer',
    avatar: 'https://i.pravatar.cc/150?u=jordan',
    bio: 'Specialist in Tailwind CSS and interactive components.'
  }
]
</script>

<template>
  <div class="space-y-12">
    <UPageHero
      title="Our Story & Mission"
      description="We're on a mission to simplify web development by providing the most robust and elegant starter templates for Nuxt developers worldwide."
      :links="[{
        label: 'View Features',
        to: '/#features',
        color: 'neutral',
        variant: 'subtle'
      }]"
    />

    <UPageSection
      title="Our Core Values"
      description="The principles that guide our daily work and long-term vision."
    >
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6">
        <UCard v-for="value in values" :key="value.title" class="group hover:ring-2 hover:ring-primary transition-all duration-300">
          <template #header>
            <div class="flex items-center gap-3">
              <div class="p-2 rounded-lg bg-primary/10 text-primary group-hover:bg-primary group-hover:text-white transition-colors">
                <UIcon :name="value.icon" class="text-2xl" />
              </div>
              <h3 class="font-bold text-lg">{{ value.title }}</h3>
            </div>
          </template>
          <p class="text-sm text-gray-600 dark:text-gray-400">
            {{ value.description }}
          </p>
        </UCard>
      </div>
    </UPageSection>

    <UPageSection
      title="Meet the Team"
      description="The talented individuals behind the Nuxt Starter Template."
      variant="subtle"
      class="rounded-3xl"
    >
      <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-8">
        <div v-for="member in team" :key="member.name" class="flex flex-col items-center text-center space-y-4 p-6 bg-white dark:bg-gray-900 rounded-2xl shadow-sm border">
          <UAvatar
            :src="member.avatar"
            :alt="member.name"
            size="3xl"
            class="ring-4 ring-primary/10"
          />
          <div>
            <h4 class="text-xl font-bold">{{ member.name }}</h4>
            <p class="text-primary font-medium text-sm">{{ member.role }}</p>
          </div>
          <p class="text-sm text-gray-500 max-w-[200px]">
            {{ member.bio }}
          </p>
          <div class="flex gap-2">
            <UButton icon="i-simple-icons-x" color="neutral" variant="ghost" size="xs" />
            <UButton icon="i-simple-icons-linkedin" color="neutral" variant="ghost" size="xs" />
            <UButton icon="i-simple-icons-github" color="neutral" variant="ghost" size="xs" />
          </div>
        </div>
      </div>
    </UPageSection>

    <UPageCTA
      title="Want to join our team?"
      description="We are always looking for passionate developers and designers to join our growing community."
      variant="subtle"
      :links="[{
        label: 'Careers',
        to: '/contact',
        color: 'primary',
        trailingIcon: 'i-heroicons-arrow-right'
      }]"
    />
  </div>
</template>
