<template>
  <div>
    <!-- Food Section -->
    <h1>Food</h1>
    <food-item />
    <food-item2 />

    <!-- Personal Profile Section -->
    <h1>Personal Profile</h1>
    <personal-profile />

    <!-- Comments Section -->
    <h1>Comments</h1>
    <comment-form />
    <comment />

    <!-- RestApi Section -->
    <rest-api/> 
  </div>
</template>

<script setup>
/* Import all components with correct paths and case-sensitive names */
import FoodItem from './components/FoodItem.vue'
import FoodItem2 from './components/FoodItem2.vue'
import PersonalProfile from './components/PersonalProfile.vue'
import CommentForm from './components/CommentForm.vue'
import Comment from './components/Comment.vue'
import RestApi from './components/RestApi.vue'
</script>

<style>
h1 {
  margin-top: 2rem;
  margin-bottom: 1rem;
  color: #ff0055; 
  font-family: 'Orbitron', sans-serif;
}
</style>
