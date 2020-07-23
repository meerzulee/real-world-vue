<template>
  <div>
    <h1>Event listing for {{ user.user.name }}</h1>
    <EventCard v-for="event in event.events" :key="event.id" :event="event" />
    <template v-if="page != 1">
      <router-link
        :to="{ name: 'event-list', query: { page: page - 1 } }"
        rel="prev"
        >Prev page</router-link
      >
    </template>
    |
    <template>
      <router-link
        v-for="(item, index) in $store.getters.totalPage"
        :key="index"
        :to="{ name: 'event-list', query: { page: index + 1 } }"
        rel="prev"
        style="margin: 0 4px"
        >{{ index + 1 }}</router-link
      >
    </template>
    |
    <template v-if="page != $store.getters.totalPage">
      <router-link
        :to="{ name: 'event-list', query: { page: page + 1 } }"
        rel="next"
        >Next page</router-link
      >
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
    this.$store.dispatch('event/fetchEvents', {
      perPage: 3,
      page: this.page
    })
  },
  computed: {
    page() {
      return parseInt(this.$route.query.page) || 1
    },
    ...mapState(['event', 'user'])
  }
}
</script>

<style scoped>
.router-link-exact-active {
  color: blue;
}
</style>
