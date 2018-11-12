<template>
      <div>
        <h1>Events Listing</h1>
        <EventCard/>
        <BaseButton></BaseButton>
      </div>
    </template>

<script>
import EventCard from '@/components/EventCard.vue'
export default {
  components: {
    EventCard
  }
}
</script>
