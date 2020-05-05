<template>
  <div>
    <h1>Events</h1>
    <EventCard
      v-for="(event, index) in events"
      :key="index"
      :event="event"
      :data-index="index"
    />
  </div>
</template>
<script>
import { mapState } from 'vuex'
import EventCard from '@/components/EventCard.vue'
export default {
  components: {
    EventCard
  },
  async fetch({ store, error }) {
    try {
      await store.dispatch('events/fetchEvents')
    } catch (err) {
      error({
        statusCode: 503,
        message: 'Something went wrong' + err.message
      })
    }
  },
  computed: mapState({
    events: (state) => state.events.events
  }),
  head() {
    return {
      title: 'Listing Events'
    }
  }
}
</script>
