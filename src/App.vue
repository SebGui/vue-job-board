<template>
  <div class="app">
    <MyHeader :order="order" @updateOrder="termUpdated"/>

    <JobList :jobs="jobs" :order="order"/>
  </div>
</template>

<script setup lang="ts">
// Core methods
import { ref } from 'vue';

// Custom Type/Interface
import Job from './types/Job'
import OrderTerm from './types/OrderTerm'

// Component
import JobList from './components/JobList.vue'
import MyHeader from './components/MyHeader.vue'


/* Jobs dummy data */
const jobs = ref<Job[]>([
  {title:"Frontend Developer", location: "Paris", salary: 60000, id:1},
  {title:"Backend Developer", location: "Marseille", salary: 60000, id:2},
  {title:"DevOps Engineer", location: "Toulouse", salary: 65000, id:3},
  {title:"QA Engineer", location: "Lyon", salary: 55000, id:4},
  {title:"CTO", location: "Lille", salary: 70000, id:5}
])

/* Initialize order term */
const order = ref<OrderTerm>('title')

/* Term Updater */
const termUpdated = (term: OrderTerm) => {
  //console.log(`Term updated : ${term}`);
  order.value = term;
}

</script>

<style></style>
