<script setup>
import { ref, onMounted } from 'vue'
import { supabase } from '../supabase/client'

const loading = ref(true)
const errorMessage = ref(null)
const instruments = ref([])

onMounted(async () => {
  // Simple test query to the "instruments" table
  const { data, error } = await supabase
    .from('instruments')
    .select('*')

  if (error) {
    console.error('Supabase error:', error)
    errorMessage.value = error.message
  } else {
    instruments.value = data || []
  }

  loading.value = false
})
</script>

<template>
  <div>
    <h2>Supabase Connection Test</h2>

    <p v-if="loading">Checking connection...</p>
    <p v-else-if="errorMessage">
      ❌ Error: {{ errorMessage }}
    </p>
    <div v-else>
      <p>✅ Connected! Fetched {{ instruments.length }} instruments:</p>
      <ul>
        <li v-for="instrument in instruments" :key="instrument.id">
          {{ instrument.id }} – {{ instrument.name }}
        </li>
      </ul>
    </div>
  </div>
</template>
