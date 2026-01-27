<template>
  <section class="section section-dark">
    <div class="container">
      <h2 class="section-title">Comments</h2>

      <div class="comments-list">
        <div
          v-for="c in comments"
          :key="c.id"
          class="comment-item"
        >
          <h4>{{ c.name }}</h4>
          <p>{{ c.comment }}</p>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { supabase } from '../lib/supabaseClient'

const comments = ref([])

async function getComments() {
  const { data, error } = await supabase
    .from('comments')
    .select()
    .order('id', { ascending: false })

  if (!error) {
    comments.value = data
  }
}

onMounted(() => {
  getComments()
})
</script>

<style scoped>
.comments-list {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: calc(var(--spacing-unit) * 3);
}

.comment-item {
  background: var(--card-bg);
  padding: calc(var(--spacing-unit) * 3);
  border-radius: 12px;
  border: 1px solid rgba(255, 0, 85, 0.25);
  transition: all 0.3s ease;
}

.comment-item:hover {
  border-color: var(--neon-red);
  box-shadow: 0 0 20px rgba(255, 0, 85, 0.35);
  transform: translateY(-5px);
}

.comment-item h4 {
  color: var(--neon-red-bright);
  margin-bottom: 6px;
}

.comment-item p {
  color: var(--text-secondary);
}
</style>
