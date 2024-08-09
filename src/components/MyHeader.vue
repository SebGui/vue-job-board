<template>
    <div>
        <header>
          <div class="title">
            <img src="@/assets/jobImg.jpg" alt="Job picture" class="jobImg">
            <h1>Job Board</h1>
          </div>

          <div class="order">
            <button @click="handleClick('title')">Order by title</button>
            <button @click="handleClick('salary')">Order by salary</button>
            <button @click="handleClick('location')">Order by location</button>
          </div>
        </header>
    </div>
</template>

<script setup lang="ts">
/* Core Methods */
import { defineEmits } from 'vue'

/* Type import for term management */
import OrderTerm from '@/types/OrderTerm'


/* Define our emit signature */
const emit = defineEmits<{
  (e: 'updateOrder', term: OrderTerm): void
}>()

/* Click handler to set order to corresponding term */
const handleClick = (term: OrderTerm) => {
  // Emits an event to update term from App and pass it down to JobList
  emit('updateOrder', term);
}
</script>

<style scoped>
  header {
    text-align: center;
  }
  header .order {
    margin-top: 20px;
  }
  button {
    margin: 0 10px;
    color: #1195c9;
    border: 3px solid #1195c9;
    background: #d5f0ff;
    padding: 8px 16px;
    border-radius: 4px;
    cursor: pointer;
    font-weight: bold;
  }
  .jobImg {
    height: 100px;
    width: 200px;
  }
  .title {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: space-evenly;
  }
</style>