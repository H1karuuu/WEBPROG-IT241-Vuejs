<template>
  <section class="section section-dark">
    <div class="container">
      <h2 class="section-title">Leave a Comment</h2>

      <div class="comment-card">
        <form @submit.prevent="submitComment">
          <input
            type="text"
            v-model="name"
            placeholder="Your Name"
            required
          />

          <textarea
            v-model="comment"
            placeholder="Your Comment"
            rows="4"
            required
          ></textarea>

          <button type="submit" class="btn btn-primary">
            Submit
          </button>

          <p v-if="submissionStatus" class="comment-status">
            {{ submissionStatus }}
          </p>
        </form>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue'
import { supabase } from '../lib/supabaseClient'

const name = ref('')
const comment = ref('')
const submissionStatus = ref(null)

async function submitComment() {
  submissionStatus.value = 'Submitting...'

  const { error } = await supabase
    .from('comments')
    .insert([{ name: name.value, comment: comment.value }])

  if (error) {
    console.error(error)
    submissionStatus.value = 'Error submitting comment. Please try again.'
  } else {
    submissionStatus.value = 'Comment submitted successfully!'
    name.value = ''
    comment.value = ''
  }
}
</script>

<style scoped>
.comment-card {
  background: var(--card-bg);
  padding: calc(var(--spacing-unit) * 4);
  border-radius: 12px;
  border: 1px solid rgba(255, 0, 85, 0.25);
  box-shadow: 0 0 20px rgba(255, 0, 85, 0.15);
  max-width: 600px;
  margin: 0 auto;
}

.comment-card input,
.comment-card textarea {
  width: 100%;
  margin-bottom: 12px;
  padding: calc(var(--spacing-unit) * 2);
  background: rgba(0, 0, 0, 0.6);
  border: 1px solid rgba(255, 0, 85, 0.4);
  border-radius: 8px;
  color: var(--text-primary);
}

.comment-card input:focus,
.comment-card textarea:focus {
  outline: none;
  border-color: var(--neon-red);
  box-shadow: 0 0 12px rgba(255, 0, 85, 0.4);
}

.comment-status {
  margin-top: 10px;
  color: var(--neon-red-bright);
}
</style>
