<script setup>
const contactMethods = [
  {
    name: 'Email Us',
    description: 'Our team is here to help with any technical questions.',
    value: 'hello@nuxt-starter.dev',
    icon: 'i-heroicons-envelope',
    to: 'mailto:hello@nuxt-starter.dev'
  },
  {
    name: 'Visit Us',
    description: 'Come say hi at our headquarters in the heart of tech.',
    value: '123 Nuxt Lane, Vue City, 94103',
    icon: 'i-heroicons-map-pin',
    to: '#'
  },
  {
    name: 'Call Us',
    description: 'Mon-Fri from 8am to 5pm PST for urgent support.',
    value: '+1 (555) 000-0000',
    icon: 'i-heroicons-phone',
    to: 'tel:+15550000000'
  }
]

const form = reactive({
  name: '',
  email: '',
  subject: '',
  message: ''
})

const subjects = ['General Inquiry', 'Technical Support', 'Partnership', 'Feedback']

const isLoading = ref(false)

async function onSubmit() {
  isLoading.value = true
  // Simulate API call
  await new Promise(resolve => setTimeout(resolve, 1500))
  alert('Message sent successfully!')
  isLoading.value = false
  form.name = ''
  form.email = ''
  form.subject = ''
  form.message = ''
}
</script>

<template>
  <div class="space-y-12">
    <UPageHero
      title="Get in Touch"
      description="Have questions? We'd love to hear from you. Send us a message and we'll respond as soon as possible."
    />

    <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">
      <!-- INFO COLUMN -->
      <div class="lg:col-span-1 space-y-6">
        <h2 class="text-2xl font-bold mb-4">Contact Information</h2>
        
        <UCard 
          v-for="method in contactMethods" 
          :key="method.name" 
          class="hover:border-primary transition-colors"
          :ui="{ body: 'p-5' }"
        >
          <div class="flex gap-4">
            <div class="shrink-0 p-3 rounded-full bg-primary/10 text-primary">
              <UIcon :name="method.icon" class="text-xl" />
            </div>
            <div>
              <p class="font-bold text-sm">{{ method.name }}</p>
              <p class="text-xs text-gray-500 mb-2">{{ method.description }}</p>
              <NuxtLink :to="method.to" class="text-primary font-medium hover:underline">
                {{ method.value }}
              </NuxtLink>
            </div>
          </div>
        </UCard>

        <div class="pt-6">
          <p class="font-semibold mb-4">Follow Us</p>
          <div class="flex gap-3">
            <UButton icon="i-simple-icons-x" color="neutral" variant="subtle" />
            <UButton icon="i-simple-icons-github" color="neutral" variant="subtle" />
            <UButton icon="i-simple-icons-discord" color="neutral" variant="subtle" />
          </div>
        </div>
      </div>

      <!-- FORM COLUMN -->
      <div class="lg:col-span-2">
        <UCard class="shadow-lg border-2 border-primary/5">
          <template #header>
            <h3 class="text-xl font-bold">Send us a Message</h3>
          </template>

          <UForm :state="form" @submit="onSubmit" class="space-y-6">
            <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
              <UFormField label="Full Name" name="name" required>
                <UInput v-model="form.name" placeholder="John Doe" icon="i-heroicons-user" class="w-full" />
              </UFormField>

              <UFormField label="Email Address" name="email" required>
                <UInput v-model="form.email" type="email" placeholder="john@example.com" icon="i-heroicons-at-symbol" class="w-full" />
              </UFormField>
            </div>

            <UFormField label="Subject" name="subject" required>
              <USelectMenu v-model="form.subject" :items="subjects" placeholder="Choose a subject" class="w-full" />
            </UFormField>

            <UFormField label="Message" name="message" required>
              <UTextarea v-model="form.message" placeholder="How can we help you?" :rows="6" class="w-full" />
            </UFormField>

            <div class="flex justify-end">
              <UButton 
                type="submit" 
                color="primary" 
                size="lg" 
                :loading="isLoading"
                trailing-icon="i-heroicons-paper-airplane"
              >
                Send Message
              </UButton>
            </div>
          </UForm>
        </UCard>
      </div>
    </div>

    <!-- FAQ SECTION -->
    <UPageSection
      title="Frequently Asked Questions"
      description="Quick answers to common questions about our template."
      variant="subtle"
      class="rounded-3xl"
    >
      <UAccordion
        :items="[
          { label: 'Is this template free to use?', content: 'Yes, this starter template is open-source and free for both personal and commercial projects.' },
          { label: 'How do I update Nuxt UI?', content: 'You can update by running npm install @nuxt/ui@latest in your terminal.' },
          { label: 'Do you offer custom development?', content: 'While we focus on templates, our core team is available for consulting on large-scale Nuxt projects.' }
        ]"
      />
    </UPageSection>
  </div>
</template>
