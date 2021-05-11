<template>
  <div class="notification-container">
    <NotificationBar
      v-for="(notification, index) in notifications"
      :key="index"
      :notification="notification"
    />
  </div>
</template>

<script>
import NotificationBar from '@/components/NotificationBar.vue'
import { mapState } from 'vuex'

export default {
  components: {
    NotificationBar,
  },

  computed: {
    ...mapState('notification', ['notifications']),
  },
}
</script>

<style scoped>
.notification-container {
  position: fixed;
  bottom: 0;
  right: 0;
  padding-right: 40px;
}
</style>