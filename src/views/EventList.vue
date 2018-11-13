<template>
      <div>
        <h1>Events Listing</h1>
        <EventCard v-for="event in events" :key="event.id" :event="event"/>
        <BaseButton></BaseButton>
        <template v-if="page != 1">
          <router-link :to="{ name: 'event-list', query: { page: page - 1 } }" rel="prev">Prev Page</router-link> | 
        </template>
        <template v-if="showNexPage" >
        <router-link :to="{ name: 'event-list', query: { page: page + 1 } }">Next Page</router-link>
        </template>
      </div>
    </template>

<script>
import EventCard from '@/components/EventCard.vue'
import { mapState } from 'vuex'

export default {
  components: {
    EventCard
  },
  created() {
    this.$store.dispatch('fetchEvents', {
      perPage: 3, // <-- How many items to display per page
      page: this.page // <-- What page we're on
    })
    console.log('showNextPage = ' + this.showNexPage)
  },
  computed: {
    page() {
      // What page we're currently on
      return parseInt(this.$route.query.page) || 1
    },
    showNexPage() {
      return parseInt(this.total_events - this.page * 3) > 0
    },
    ...mapState(['events', 'total_events'])
  }
}
</script>
