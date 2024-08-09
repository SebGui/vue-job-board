<template>
    <div class="job-list">
        <p>Ordered by : {{ order }}</p>
        <transition-group name="list" tag="ul">
            <li v-for="job in orderJobs" :key="job.id">
                <h2>{{ job.title }} in {{ job.location }}</h2>
                <div class="salary">
                    {{ job.salary }} €
                </div>
                <div class="description">Lorem ipsum dolor sit amet consectetur adipisicing elit. Est facere officiis quidem consectetur illo vitae reprehenderit fugit placeat. Optio nulla exercitationem, quasi iste tempore, vel quia, consequatur nobis unde tempora dolorum! Hic cum necessitatibus iure officiis odit soluta sed, voluptates a. Saepe eos ullam, cumque fuga quos quas nesciunt quisquam reprehenderit neque esse, sit consequuntur dolor nulla porro cum corrupti eum eligendi eius alias illum? Quod, voluptas error fuga delectus accusantium nemo ratione quisquam minus dolor amet voluptates velit. Placeat at maiores asperiores corrupti quae error enim veritatis repellat pariatur, aperiam ullam assumenda quis veniam, consequuntur, sequi mollitia autem repudiandae!</div>
            </li>
        </transition-group>
    </div>
</template>

<script setup lang="ts">
// Core Methods
import { PropType, defineProps, computed } from 'vue'

// Custom type/interface
import Job from '@/types/Job'
import OrderTerm from '@/types/OrderTerm'


/* Define our props with type */
const props = defineProps({
    jobs : {
        required: true,
        type: Array as PropType<Job[]> // Set our jobs to conform to our Job interface
    },
    order: {
        required:true,
        type: String as PropType<OrderTerm> // Only allow our 3 types from OrderTerm custom type
    }
})

/* Order Jobs with computed */
const orderJobs = computed(() => {
    // Do not directly sort the base array, use .sort() (or else) on spreaded array
    return [...props.jobs].sort((a: Job, b: Job) => {
        // 1 = switch / -1 = don't switch
        return a[props.order] > b[props.order] ? 1 : -1
    })
})

</script>

<style scoped>
  /* Job list CSS */
  .job-list {
    max-width: 960px;
    margin: 40px auto;
  }
  .job-list ul {
    padding: 0;
  }
  .job-list li {
    list-style-type: none;
    background: white;
    padding: 16px;
    margin: 16px 0;
    border-radius: 4px;
  }
  .job-list h2 {
    margin: 0 0 10px;
    text-transform: capitalize;
  }

  /* Salary CSS*/
  .salary {
    display: flex;
    color: #17bf66;
    font-weight: bold;
    margin: 10px 4px;
  }
  .salary img {
    width: 30px;
  }

  /* List transition */
  .list-move {
    transition: all 1s;
  }
</style>